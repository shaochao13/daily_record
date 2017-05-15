基本概念：

+ 镜像 Image
+ 容器 Container
+ 仓库 Repository

## Image
`Image` 是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。不包含任何动态数据，其内容在构建之后也不会被改变。  采用`分层存储`设计。

`虚悬镜像(dangling image)` :

    由于新旧镜像同名，旧镜像名称被取消，从而出现仓库名、标签名为<none>的镜像。
    可以命令: docker images -f dangling=true  可以专门jogi这类镜像
    删除此类镜像命令: docker rmi $(docker images -q -f dangling=true)

## Docker Registry
    一个集中的存储、分发Image的服务。
一个Docker Registry 中可以包含多个仓库(Repository)，每个仓库可以包含多个标签(`Tag`),每个Tag对应一个`Image`。

通常，一个`Repository`会包含同一个软件不同版本的`Image`，而`Tag`就常用于对应该软件的各个版本。可以通过`<仓库名>:<标签>`的格式来指定具体是这个软件的哪个版本的Image。如果不给出标签，将以`latest` 作为默认标签。

`仓库名`经常以`两段路径`形式出现：如`jwilder/nginx-proxy`,前者往往意味着Docker Registry 多用户环境下的用户名，后者则往往是对应的软件名。


