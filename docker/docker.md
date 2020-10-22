基本概念：

+ 镜像 Image
+ 容器 Container
+ 仓库 Repository

鏡像(Image) 设计为`分层存储`的架构，由多层文件系统联合组成。镜像构建时，会一层层构建，前一层是后一层的基础。每一层构建完就不会再发生改变，后一层上的任何改变只发生在自己这一层。*`因此，在构建镜像的时候，需要额外小心，每一层尽量只包含该层需要添加的东西，任何额外的东西应该在该层构建结束前清理掉。`*

`容器Container` 也是使用的是`分层存储`,每一个容器运行时，是以镜像为基础层，在其上创建一个当前容器的存储层，可以称这个为容器运行时读写而准备的存储层为容器存储层。  容器存储层的生存周期和容器一样，容器消亡时，容器存储层也随之消亡。因此，任何保存于容器存储层的信息都会随容器删除而丢失。

*`容器不应该向其存储层内写入任何数据，容器存储层要保持无状态化。所有的文件写入操作，都应该使用数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主(或网络存储)发生读写，其性能和稳定性更高`*

镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的 `类` 和 `实例`一
样，`镜像是静态的定义，容器是镜像运行时的实体`。容器可以被创建、启动、停止、删除、
暂停等。

`容器 Container` 的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的命
名空间。因此容器可以拥有自己的 root 文件系统、自己的网络配置、自己的进程空间，甚
至自己的用户ID空间。容器内的进程是运行在一个隔离的环境里，使用起来，就好像是在一
个独立于宿主的系统下操作一样。

## Image
+ `Image` 是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。不包含任何动态数据，其内容在构建之后也不会被改变。  采用`分层存储`设计。

*Image* 的唯一标识是ID和摘要(disgest)

+ `虚悬镜像(dangling image)` :

    由于新旧镜像同名，旧镜像名称被取消，从而出现仓库名、标签名为<none>的镜像。

    可以命令: 
    ```bash
    docker images -f dangling=true
    ```
    可以专门显示这类镜像

    删除此类镜像命令: 
    ```bash
    docker image prune # Docker 1.13+ 版本中使用
    
    docker rmi $(docker images -q -f dangling=true) #1.13之前版本执行
    ```

+ 中间层镜像  
  
    无标签的镜像，是其他镜像所依赖的镜像。

`docker images -a`  列出所有镜像，包括中间层镜像

`docker images` 只会列出所有顶级镜像。`docker image ls` 在Docker 1.13+中推荐使用。

+ 保存 image
```bash
# 把nginx 镜像 保存到"nginx.tar.gz"文件中
docker image save nginx | gzip > nginx.tar.gz
```

+ 加载 image
```bash
docker image load -i nginx.tar.gz
```

+ 删除 image
```bash
docker rmi [选项] <镜像1> [<镜像2> ...]
docker image rm # Docker 1.13+ 推荐使用
```

## Dockerfile 制定镜像
1. `FROM` 指定基础镜像，在其上进行定制。比如：`FROM nginx` 表示以nginx为基础镜像。

    名为`scratch`是一个特殊的镜像，它表示一个空白的镜像。如果以`scratch`为基础镜像的话，意味着不以任何镜像为基础。

    使用 `docker image build [option] <上下文路径/URL/->` 来进行定制镜像。

    例如：`docker build -t nginx:v3 .`
    
2. `RUN`  用来执行命令行命令。 

    有两种格式：

    + `shell`格式：`RUN <命令>` ,就像直接在命令行中输入的命令一样。
    
        例如：`RUN echo '<h1>hello,Docker!</h1>' > /usr/share/nginx/html/index.html`

    + `exec`格式：`RUN [“可执行文件”， “参数1”，“参数2”]` ,这更像是在函数调用中的格式 

    Dockerfile中的每一个指令都会建立一层，RUN也不例外。`Union FS`有最大层数的限制，现在是不得超过***127***层。

3. `COPY` 复制文件 ， 会保留源文件的各种元数据。

    格式：
    + `COPY <源路径> ...  <目标路径>`
    + `COPY ["<源路径1>",...  "<目标路径>"]`

    <源路径>可以是多个，甚至可以是通配符，例如：
    ```
    COPY hom* /mydir/
    COPY hom?.txt /mydir/
    ```
    <目标路径>可以是容器内的绝对路径，也可以是相对于工作目录的相对路径(工作目录可以用`WORKDIR`指令来指定)。

4. `ADD` 更高级的复制文件，仅在需要自动 解压缩的场合中使用。  如果<源路径>为一个tar压缩文件的话，压缩格式为gzip,bzip2以及xz的情况下，`ADD`指令将会自动解压缩这个压缩文件到<目标路径>去。`最适合使用ADD的场合，就是所提及的需要自动解压缩的场合`。

需要注意的是， `ADD` 指令会令镜像构建缓存失效，从而可能会令镜像构建变得比较缓慢。
因此在 `COPY` 和 `ADD` 指令中选择的时候，可以遵循这样的原则，所有的文件复制均使用 `COPY` 指令，仅在需要自动解压缩的场合使用 `ADD` 。

5. `CMD` 容器启动命令。***容器就是进程***。容器中的应用都应该以前台执行，容器内没有后台服务的概念。例如,启动NGINX的正确做法：`CMD ["nginx", "-g", "daemon off;"]`

    格式：
    + `shell`格式：`CMD <命令>`
    + `exec` 格式：`CMD ["可执行文件",”参数1“，“参数2”,...]`

6. `ENTRYPOINT` 入口点 ，使用指令格式与`CMD`一样。

7. `ENV` 设置环境变量

    格式：
    + `ENV <key> <value>`
    + `ENV <key1>=<value1> <key2>=<value2>...`
    
    例如:
    ```
    ENV VERSION=1.0 DEBUG=on NAME="HAPPY FEET"
    ```
    ```
    ENV NODE_VERION 7.2.0
    ```
8. `ARG` 构建参数 ---待完

9. `VOLUME` 定义匿名卷

    例如：
    ```
    VOLUME /data
    ```
    这里的/data 目录就会在运行时自动挂载为匿名卷，任何向/data中写入的信息都不会记录进容器存储层，从而保证了容器存储层的无状态化。
    
    当然也可以在运行时覆盖这个挂载设置：
    ```
    docker run -d -v mydata:/data XXXX
    ```
    这命令中就使用了`mydata`这个命名卷挂载到了/data这个位置，替代了Dockerfile中定义的匿名卷的挂载配置。


    格式：
    + `VOLUME ["<路径1>","<路径2>",...]`
    + `VOLUME <路径>` 

10. `EXPOSE` 声明端口

    格式：`EXPOSE <端口1> [<端口2> ...]`

    与在运行时使用的`-p <宿主端口>:<容器端口>` 不一样，`-p`是映射宿主端口和容器端口，是将容器的对应端口服务公开给外界访问。`EXPOSE`仅仅是声明容器打算使用什么端口而已，并不会自动在宿主进行端口映射。

11. `WORKDIR` 指定工作目录

    格式：`WORKDIR <工作目录路径>`

    如果需要改变以后各层的工作目录位置，就应该使用`WORKDIR`指令。如果指定的目录不存在，会进行创建。

12. `USER` 指定当前用户
    
    格式：`USER <用户名>`

    如果指定的用户不存在，则无法进行切换。

13. `HEALTHCHECK` 健康检查，判断容器的状态是否正常

    格式：
    + `HEALTHCHECK [选项] CMD <命令>` 设置检查容器健康状况的命令
    + `HEALTHCHECK NONE` 屏蔽掉其健康检查指令

14. `ONBUILD` 当以当前镜像为基础镜像时，构建下一级镜像时才会执行。

```dockerfile
FROM django
# RUN apt-get update && apt-get install python3-pip
# 添加宿主的文件或目录到容器中
# ADD ./data  /home/data
# COPY ./data.tar /home
# 指定环境变量
# ENV itcast=python
# 指定进入容器中所在目录，工作目录
WORKDIR /home
RUN django-admin startproject test
WORKDIR /home/test
# 对外开放端口
EXPOSE 8000
# 容器启动后执行的命令
ENTRYPOINT python3 manage.py runsever 0.0.0.0:8000
```

```shell
# 根据上面提供的Dockerfile文件制作容器命令：
docker build -t container_name /Dockerfile_dir
```




## Docker Registry
    一个集中的存储、分发Image的服务。
一个Docker Registry 中可以包含多个仓库(Repository)，每个仓库可以包含多个标签(`Tag`),每个Tag对应一个`Image`。

通常，一个`Repository`会包含同一个软件不同版本的`Image`，而`Tag`就常用于对应该软件的各个版本。可以通过`<仓库名>:<标签>`的格式来指定具体是这个软件的哪个版本的Image。如果不给出标签，将以`latest` 作为默认标签。

`仓库名`经常以`两段路径`形式出现：如`jwilder/nginx-proxy`,前者往往意味着Docker Registry 多用户环境下的用户名，后者则往往是对应的软件名。


## Docker 容器

使用`docker inspect` 可以查看容器的信息

### 获取镜像
```
docker image pull [选项] [Docker Registry地址]<仓库名>:<标签>
```

### 启动容器
+ 基于镜像新建一个容器并启动

    `docker container run`
+ 将在终止状态(stopped)的容器重新启动

    `docker container start`

+ 后台(background) 运行  

    让Docker在后台运行而不是直接把执行命令的结果输出在当前宿主机下。

    通过添加`-d` 参数实现。

+ 自定义容器的名称

    ```bash
    docker container run -d -P --name web training/webapp python app.py
    ```



**常用可选参数说明**：

- `-i` 表示以“交互模式”运行容器。
- `-t` 表示容器启动后会进入其命令行。加入`-it` 这两个参数后，容器创建就能登录进去，即分配一个伪终端。
- `--name` 为创建的容器命名。
- `-v` 表示目录映射关系，格式：**宿主机目录:容器中目录**。注意：最好做目录映射，在宿主机上做修改，然后共享到容器上。
- `-d` 会创建一个守护式容器在后台运行(这样创建容器后不会自动登录容器)
- `-p` 表示端口映射， 格式：**宿主机端口:容器中端口**。
- `--network=host` 表示将主机的网络环境映射到容器中，使容器的网络与主机相同。



### 终止容器

    docker stop

### 进入容器

    docker attach 或者使用 nsenter 工具

### 导出和导入容器

+ 导出：
  
    `docker export`

    例如： `docker export 容器ID > XXX.tar`

+ 导入：
  
    `docker import` ,导入的为容器快照，快照文件将丢弃所有的历史记录和元数据信息，即仅保存容器当时的快照状态。
    
    `docker load` ,导入镜像存储文件，存储文件将保存完整记录，何种也要大。

    例如：`cat xxx.tar | docker import - test/ubuntu:v1.0`

### 删除容器

    docker rm   ,默认不会删除正在运行中的容器。
    如果要删除一个运行中的容器，可以添加 -f 参数。

### 清理所有处于终止状态的容器

    docker rm $(docker ps -a -q)



## 私有仓库

`docker-registry` 是官方提供的工具，可以用于构建私有的镜像仓库。

通过获取官方 `registry` 镜像来运行:

```bash
docker run -d -p 5002:5000 -v /opt/data/registry:/var/lib/registry --name registry_local  registry
docker run --network=host -v /opt/data/registry:/var/lib/registry --name registry_local registry
# --network=host 这样可以让容器共享宿主机的网卡
```

使用 `docker image tag` 将一个已经下载的镜像标记到私有仓库，如 将 `ubuntu:latest` 这个镜像标记为 `127.0.0.1:5000/ubuntu:latest`（格式为`docker image tag IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]NAME[:TAG]`）。

```bash
docker image tag ubuntu:latest 127.0.0.1:5000/ubuntu:latest
docker tag ubuntu:latest 127.0.0.1:5000/ubuntu:latest
```

使用 `docker image push` 上传标记的镜像。

```bash
docker image push 127.0.0.1:5000/ubuntu:latest
docker push 127.0.0.1:5000/ubuntu:latest
```

然后，可以使用 `http://127.0.0.1:5002/v2/_catalog` 或者使用 `curl 127.0.0.1:5002/v2/_catalog` 来查看本地私有仓库中的信息。

从本地私有仓库拉取镜像资源：

```shell
docker pull 127.0.0.1:5000/ubuntu:latest
```



## Docker 数据管理

### 在容器中管理数据主要有两种方式：

+ 数据卷(`Data volumes`)

    特性：
    ```
    1. 数据卷可以在容器之间共享和重用
    2. 对数据卷的修改会立马生效
    3. 对数据卷的更新，不会影响镜像
    4. 数据卷默认会一直存在，即使容器被删除
    ```

    创建一个数据卷：
    ```bash
    docker volume create my-vol
    ```

    查看所有的数据卷：
    ```bash
    docker volume ls
    ```

    查看指定数据卷的信息:
    ```bash
    docker volume inspect my-vol
    ```

    删除数据卷:
    ```bash
    docker volume rm my-vol
    ```

    删除无主的数据卷:
    ```bash
    docker volume prune
    ```

    挂载一个主机`目录`作为数据卷 (`--mount or -v`):

    本地目录的路径必须是绝对路径，如果目录不存在Docker会自动为你创建它
    
    ```shell
    docker run -dit --name 容器名称 -v 宿主机目录:容器内目录 镜像名称 [命令]
    ```
    
    ```bash
    docker run -d -P --name web  \
    ```
# -v /src/webapp:/opt/webapp \
    --mount type=bind,source=/src/webapp,target=/opt/webapp \
    training/webapp \
    python app.py
    ```
    
    Docker挂载主机目录的默认权限是读写，用户也可以通过增加 `readonly` 指定为只读:
    ```bash
    docker run -d -P --name web  \
# -v /src/webapp:/opt/webapp \
    --mount type=bind,source=/src/webapp,target=/opt/webapp,readonly  \
    training/webapp \
    python app.py
    ```
    
    挂载一个本地主机文件作为数据卷:
    ```bash
    docker run --rm -it \
    --mount type=bind,source=~/.bash_history,target=/root/.bash_history \
    ubuntu:17.10 \
    bash
    ```

+ 数据卷容器(`Data volume containers`) *专门用来提供数据卷供其它容器挂载的。*

    **创建一个数据卷容器的命令格式：**

    ```bash
    docker create -v 容器数据卷目录 --name 容器名称 镜像名称 [命令]
    ```

    例如,创建一个名为dbdata的数据卷容器：

    ```bash
    docker create -v /dbdata --name dbdata ubuntu /bin/bash
    
    docker run -d -v /dbdata --name dbdata training/postgres echo Data-only container for postgres
    ```
```
    
**其他容器，同时挂载数据卷容器的命令格式：**
    
    ```bash
    docker run --volumes-from 数据卷窗口id/name -tid --name 容器名称 镜像名称 [命令]
    
    
    docker run -d --volumes-from dbdata --name myu ubuntu /bin/bash
```


​    
​    在其他容器中使用 `--volumes-from` 来挂载`dbdata`容器中的数据卷：
​    
    ```bash
    docker run -d --volumes-from dbdata --name db1 training/postgress
    docker run -d --volumes-from dbdata --name db2 training/postgress
    ```
    
    也可以从其他已挂载了数据卷的容器来`级联挂载`数据卷：
    
    ```bash
    docker run -d --name db3 --volumes-from db1  /postgress
    ```

### 备份数据卷

首先使用`--volumes-from` 标记来创建一个加载dbdata容器卷的容器，并从主机挂载当前目录到容器的/backup目录。例如：

```bash
docker run --volumes-from dbdata -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
```

容器启动后，使用了`tar`命令来将dbdata卷备份为容器中的`/backup/backup.tar`文件，也就是主机当前目录下的名为backup.tar的文件。

### 恢复数据卷

首先创建一个带有空数据卷的容器dbdata2:

```bash
docker run -v /dbdata --name dbdata2 ubuntu /bin/bash
```

然后再创建另外一个容器，挂载 *dbdata2* 容器郑中的数据卷，并使用 `untar` 解压备份文件到挂载的容器卷中。

```bash
docker run --volumes-from dbdata2 -v $(pwd):/backup busybox tar xvf /backup/backup.tar
```

为了查看/验证恢复的数据，可以再启动一个容器挂载同样的容器卷来查看：

```bash
docker run --volumes-from dbdata2 busybox /bin/ls /dbdata
```

## 外部访问容器

通过 `-P` 或者 `-p` 参数来指定端口映射。

+ 使用 `-P`（大写）

    当使用 `-P` 标记时，Docker 会随机映射一个 `49000~49900` 的端口到内部容器开放的网络端口上。

    例如：

    ```bash
    docker run -d -P training/webapp python app.py
    ```
    可以使用 `docker ps -l` 查看相关的端口信息。

    可以使用 `docker logs` 命令查看应用的信息。

    ```bash
    docker logs -f + '容器ID或者容器名称'
    ```

+ 使用`-p` (小写的)

    `-p` (小写的)则可以指定要映射的端口。在一个指定端口上只可以绑定一个容器。
    支持的格式有：

    + `ip:hostPort:containerPort`   映射到指定地址的指定端口

    ```bash
    docker run -d -p 5000:5000 training/webapp python app.py
    ```

    + `ip::containerPort` 映射到指定地址的任意端口上
    ```bash
    docker run -d -p 127.0.0.1:5000:5000 training/webapp python app.py
    ```

    + `hostPort:containerPort`  映射所有接口地址
    ```bash
    docker run -d -p 127.0.0.1::5000 training/webapp python app.py
    ```

    `-p`可以多次使用来绑定多个端口:
    ```bash
    docker run -d -p 5000:5000 -p 3000:80 training/webapp python app.py
    ```

+ 查看映射端口配置

	使用`docker port` 来查看当前映射的端口配置：
    ```bash
    docker port + '容器ID或者容器name' 
    ```

### 容器互联

使用 `--link` 参数可以让容器之间安全的进行交互。

`--link` 参数的格式为： `--link name:alias` ,其中 *name* 表示要链接的容器的名称，*alias* 表示这个连接的别名。

例如：
```bash
docker run -d --name db training/postgres

docker run -d -P --name web --link db:db training/webapp python app.py
```

## 容器访问外部网络
容器要想访问外部网络，需要本地系统的转发支持。 在linux系统中，检查转发是否打开。
```bash
sysctl net.ipv4.ip_forward
# net.ipv4.ip_forward = 1 表示已经开户转发。
# 如果为0，手动开启。
sysctl -w net.ipv4.ip_forward=1
```