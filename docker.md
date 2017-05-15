基本概念：

+ 镜像 Image
+ 容器 Container
+ 仓库 Repository

## Image
1. `Image` 是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。不包含任何动态数据，其内容在构建之后也不会被改变。  采用`分层存储`设计。

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
    
2. `RUN`  用来执行命令行命令。 

    有两种格式：

    + `shell`格式：`RUN <命令>` ,就像直接在命令行中输入的命令一样。
    
        例如：`RUN echo '<h1>hello,Docker!</h1>' > /usr/share/nginx/html/index.html`

    + `exec`格式：`RUN [“可执行文件”， “参数1”，“参数2”]` ,这更像是在函数调用中的格式 

    Dockerfile中的每一个指令都会建立一层，RUN也不例外。`Union FS`有最大层数的限制，现在是不得超过***127***层。

3. 使用 `docker build [option] <上下文路径/URL/->` 来进行定制镜像。

## Docker Registry
    一个集中的存储、分发Image的服务。
一个Docker Registry 中可以包含多个仓库(Repository)，每个仓库可以包含多个标签(`Tag`),每个Tag对应一个`Image`。

通常，一个`Repository`会包含同一个软件不同版本的`Image`，而`Tag`就常用于对应该软件的各个版本。可以通过`<仓库名>:<标签>`的格式来指定具体是这个软件的哪个版本的Image。如果不给出标签，将以`latest` 作为默认标签。

`仓库名`经常以`两段路径`形式出现：如`jwilder/nginx-proxy`,前者往往意味着Docker Registry 多用户环境下的用户名，后者则往往是对应的软件名。


