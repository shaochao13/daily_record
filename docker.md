基本概念：

+ 镜像 Image
+ 容器 Container
+ 仓库 Repository

## Image
1. `Image` 是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。不包含任何动态数据，其内容在构建之后也不会被改变。  采用`分层存储`设计。

    *Image* 的唯一标识是ID和摘要(disgest)

2. `虚悬镜像(dangling image)` :

    由于新旧镜像同名，旧镜像名称被取消，从而出现仓库名、标签名为<none>的镜像。

    可以命令: `docker images -f dangling=true`  可以专门jogi这类镜像

    删除此类镜像命令: `docker rmi $(docker images -q -f dangling=true)`

3. 中间层镜像 

    无标签的镜像，是其他镜像所依赖的镜像。

    列出所有镜像，包括中间层镜像：    `docker images -a`

    `docker images` 只会列出所有顶级镜像。

## Dockerfile 制定镜像
1. `FROM` 指定基础镜像，在其上进行定制。比如：`FROM nginx` 表示以nginx为基础镜像。

    名为`scratch`是一个特殊的镜像，它表示一个空白的镜像。如果以`scratch`为基础镜像的话，意味着不以任何镜像为基础。

    使用 `docker build [option] <上下文路径/URL/->` 来进行定制镜像。

    例如：`docker build -t nginx:v3 .`
    
2. `RUN`  用来执行命令行命令。 

    有两种格式：

    + `shell`格式：`RUN <命令>` ,就像直接在命令行中输入的命令一样。
    
        例如：`RUN echo '<h1>hello,Docker!</h1>' > /usr/share/nginx/html/index.html`

    + `exec`格式：`RUN [“可执行文件”， “参数1”，“参数2”]` ,这更像是在函数调用中的格式 

    Dockerfile中的每一个指令都会建立一层，RUN也不例外。`Union FS`有最大层数的限制，现在是不得超过***127***层。

3. `COPY` 复制文件 ， 会保留源文件的各种元数据。

    格式：
    + `COPY <源路径> ...  <目标路径>`
    + `COPY ["<源路径1>",...  "<目标路径>"]`

    <源路径>可以是多个，甚至可以是通配符，例如：
    ```
    COPY hom* /mydir/
    COPY hom?.txt /mydir/
    ```
    <目标路径>可以是容器内的绝对路径，也可以是相对于工作目录的相对路径(工作目录可以用`WORKDIR`指令来指定)。

4. `ADD` 更高级的复制文件，仅在需要自动 解压缩的场合中使用。

5. `CMD` 容器启动命令。***容器就是进程***。容器中的应用都应该以前台执行，容器内没有后台服务的概念。例如,启动NGINX的正确做法：`CMD ["nginx", "-g", "daemon off;"]`

    格式：
    + `shell`格式：`CMD <命令>`
    + `exec` 格式：`CMD ["可执行文件",”参数1“，“参数2”,...]`

6. `ENTRYPOINT` 入口点 ，使用指令格式与`CMD`一样。

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

    与在运行时使用的`-p <宿主端口>:<容器端口>` 不一样，`-p`是映射宿主端口和容器端口，是将容器的对应端口服务公开给外界访问。`EXPOSE`仅仅是声明容器打算使用什么端口而已，并不会自动在宿主进行端口映射。

11. `WORKDIR` 指定工作目录

    格式：`WORKDIR <工作目录路径>`

    如果需要改变以后各层的工作目录位置，就应该使用`WORKDIR`指令。

12. `USER` 指定当前用户
    
    格式：`USER <用户名>`

    如果指定的用户不存在，则无法进行切换。

13. `HEALTHCHECK` 健康检查，判断容器的状态是否正常

    格式：
    + `HEALTHCHECK [选项] CMD <命令>` 设置检查容器健康状况的命令
    + `HEALTHCHECK NONE` 屏蔽掉其健康检查指令

14. `ONBUILD` 当以当前镜像为基础镜像时，构建下一级镜像时才会执行。


## Docker Registry
    一个集中的存储、分发Image的服务。
一个Docker Registry 中可以包含多个仓库(Repository)，每个仓库可以包含多个标签(`Tag`),每个Tag对应一个`Image`。

通常，一个`Repository`会包含同一个软件不同版本的`Image`，而`Tag`就常用于对应该软件的各个版本。可以通过`<仓库名>:<标签>`的格式来指定具体是这个软件的哪个版本的Image。如果不给出标签，将以`latest` 作为默认标签。

`仓库名`经常以`两段路径`形式出现：如`jwilder/nginx-proxy`,前者往往意味着Docker Registry 多用户环境下的用户名，后者则往往是对应的软件名。


