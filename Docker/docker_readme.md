# Docker
容器有效地将由单个操作系统管理的资源划分到孤立的组中，以便更好地在孤立的组之间平衡有冲突的资源使用需求。与虚拟化相比，这样既不需要指令级模拟，也不需要即时编译。容器可以在核心CPU本地运行指令，而不需要任何专门的解释机制。此外，也避免了准虚拟化（paravirtualization）和系统调用替换中的复杂性。    
Docker提供了各种容器管理工具（如分发、版本、移植等）让用户无需关注底层的操作，可以简单明了地管理和使用容器。用户操作Docker容器就像操作一个轻量级的虚拟机那样简单。  
可以简单地将Docker容器理解为一种沙盒（Sandbox）。每个容器内运行一个应用，不同的容器相互隔离，容器之间也可以建立通信机制。容器的创建和停止都十分快速，容器自身对资源的需求也十分有限，远远低于虚拟机。很多时候，甚至直接把容器当作应用本身也没有任何问题。

## 镜像
### 概念
Docker镜像（Image）类似于虚拟机镜像，可以将它理解为一个面向Docker引擎的只读模板，包含了文件系统。  
例如：一个镜像可以只包含一个完整的Ubuntu操作系统环境，可以把它称为一个Ubuntu镜像。  
镜像是创建Docker容器的基础。通过版本管理和增量的文件系统，Docker提供了一套十分简单的机制来创建和更新现有的镜像，用户甚至可以从网上下载一个已经做好的应用镜像，并通过简单的命令就可以直接使用。
### 基本指令
* 查看本地镜像
    `docker images`
* 移除镜像
    `docker rmi image_name`
* 修改镜像名称
    `docker tag dl.dockerpool.com:5000/ubuntu:12.04 ubuntu:12.04`

## 容器
### 概念
Docker容器（Container）类似于一个轻量级的沙箱，Docker利用容器来运行和隔离应用。
容器是从镜像创建的应用运行实例，可以将其启动、开始、停止、删除，而这些容器都是相互隔离、互不可见的。
可以把容器看做一个简易版的Linux系统环境（这包括root用户权限、进程空间、用户空间和网络空间等），以及运行在其中的应用程序打包而成的应用盒子。
镜像自身是 **只读** 的。容器从镜像启动的时候，Docker会在镜像的最上层创建一个 **可写** 层，镜像本身将保持不变。  
### 基本指令
* 运行容器
    `docker run [OPTIONS] --name container_name image_name`
    OPTIONS:
    `-d`后台运行
    `-it`通过交互式的方式运行
* 列出容器
    `docker ps [OPTIONS]`
    OPTIONS:
    `-a` 所有容器
    `-q` 容器Id
* 启停容器
    `docker stop container_id` 停止正在运行的容器
    `docker start container_id` 启动容器
    `docker restart container_id` 重启容器
* 进入容器
    `docker attach container_id`
    `docker exec container_id -it /bin/bash`
* 退出容器
    `ctl+p+q` 退出容器但不关闭
    `ctl+d` `exit` 退出容器且不关闭
* 删除容器
    `docker rm container_id`
    `docker rm $(docker ps -aq)` 删除所有已经停止的容器
* 导出导出容器
    `docker export container_id >file_name.tar`
    `cat file_name.tar | sudo docker import - container_id:tag` 注意这里导入后不再是容器而变成了镜像

## 仓库
### 概念
熟悉Git和GitHub的同学，可以很容易的理解镜像和仓库的概念。而最著名的镜像仓库就是DockerHub。
前面所说的操作`docker pull`和`docker search`其实都是本地机器向远端的服务器进行查询和拉取。默认的服务器为DockerHub。由于国内使用Docker下载各种镜像速度较慢，所以需要借助一些国内的镜像进行加速:  
* [DaoCloud 加速器地址（需要注册账号）](https://www.daocloud.io/mirror#accelerator-doc)
例如在linux执行这个脚本即可：
```
curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://c6607f77.m.daocloud.io
```
这个脚本主要干了一件事情，创建了文件：`/etc/docker/daemon.json`。文件内容为：  
```
{"registry-mirrors": ["http://c6607f77.m.daocloud.io"]}
```

### 基本指令
* 查询镜像
    `docker search image_name`
* 获取镜像
    `docker pull image_name`
* 推送镜像
    `docker push image_name`

## 数据管理
### 概念
数据卷是一个可供容器使用的特殊目录，它绕过文件系统，可以提供很多有用的特性。数据卷的使用，类似于Linux下对目录或文件进行mount操作。
### 基本指令
* 在容器内创建一个数据卷
    `docker run -it -v /my_dir ubuntu /bin/bash`
* 挂载一个主机目录或文件作为数据卷
    `docker run -it -v /host_dir:/my_dir:[option] ubuntu /bin/bash`  
    将本地主机`/host_dir`挂在到了容器中的`/my_dir`中。注意需要使用绝对路径。     
    option:`ro`只读 `rw`读写
* 从另外一个容器中挂载数据卷
    `docker run --volumes-from container_name_from --name container_name_to`  
    使得`container_name_to`能够看到`container_name_from`容器的数据卷，这样就可以实现多个容器间数据的共享和交换。

## DockerFile
Dockerfile是一个文本格式的配置文件，通过Dockerfile可以创建自动以的镜像。下面是一个简单的例子，用于搭建python运行环境。
```
# This dockerfile uses the ubuntu image
# VERSION 2 - EDITION 1
# Author: docker_user
# Command format: Instruction [arguments / command] ..
# 指定基于的基础镜像
FROM ubuntu
# 维护者信息
MAINTAINER docker_user docker_user@email.com
# 镜像的操作指令
RUN apt-get update
RUN apt-get apt-get install -y python
# 容器启动时执行指令
CMD python
```
### 基本指令
* FROM
    `FROM <image>:<tag>`指定一个基础镜像。如果在同一个Dockerfile中创建多个镜像时， 可以
使用多个FROM指令（每个镜像一次）
* MAINTAINER
    `MAINTAINER <name>`维护者信息
* RUN
    `RUN <command>` 比如`RUN apt-get update`
    `RUN["executable","param1","param2"]`比如`RUN["/bin/bash","-c","echo hello"]`
* CMD
    `CMD["executable","param1","param2"]`指定启动容器时执行的命令， 每个Dockerfile只能有一条CMD命令。
* EXPOSE
    `EXPOSE<port>[<port>...]`告诉Docker服务端容器暴露的端口号。需要在容器启动时通过`-P`或`-p`来实现端口映射
* ENV
    `ENV<key><value>` 指定一个环境变量， 会被后续RUN指令使用， 并在容器运行
时保持。
    ```
    ENV PG_MAJOR 9.3
    ENV PG_VERSION 9.3.4
    RUN curl -SL http://example.com/postgres-$PG_VERSION.tar.xz | tar -xJC /usr/src/postgress && …
    ENV PATH /usr/local/postgres-$PG_MAJOR/bin:$PATH
    ```
* ADD
    `ADD<src><dest>`该命令将复制指定的<src>到容器中的<dest>。 其中<src>可以是 *Dockerfile所在目录的* 一个相对路径（文件或目录） ； 也可以是一个URL； 还可以是一个tar文件（自动解压为目录） 。
* COPY
    `COPY<src><dest>`与`ADD`功能一样。当使用本地目录为源目录时， 推荐使用COPY。
* VOLUME
    `VOLUME["/data"]`创建一个可以从本地主机或其他容器挂载的挂载点， 一般用来存放数据库和需要保持的数据等
* ONBUILD
    配置当所创建的镜像作为其他新创建镜像的基础镜像时， 所执行的操作指令。 例如，Dockerfile使用如下的内容创建了镜像image-A。
    ```
    [...]
    ONBUILD ADD . /app/src
    ONBUILD RUN /usr/local/bin/python-build --dir /app/src
    [...]
    ```
    如果基于image-A创建新的镜像时， 新的Dockerfile中使用FROM image-A指定基础镜像时， 会自动执行ONBUILD指令内容， 等价于在后面添加了两条指令。
    使用ONBUILD指令的镜像， 推荐在标签中注明， 例如ruby： 1.9-onbuild

### 创建镜像
    `docker build -t image_name:tag docker_file_dir`

## Docker Compose
Docker Compose是一个用来定义和运行复杂应用的Docker工具。使用Compose，你可以在一个文件中定义一个多容器应用，然后使用一条命令来启动你的应用，完成一切准备工作。
* [更多说明](https://github.com/docker/compose/)
* [安装说明](https://docs.docker.com/compose/install/)
### 安装
Linux 下的安装：
```
sudo -i
curl -L https://github.com/docker/compose/releases/download/$dockerComposeVersion/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
其中`$dockerComposeVersion`表示版本号，比如下载版本 1.14.0则写为：
```
sudo -i
curl -L https://github.com/docker/compose/releases/download/1.14.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
通过执行

## 其他指令
* 显示容器的标准输出
    `docker logs image_id`

---
**参考资料**
* [Docker 加速器](http://guide.daocloud.io/dcs/daocloud-9153151.html#docker-toolbox)
* [在Windows中玩转Docker Toolbox](http://www.cnblogs.com/studyzy/p/6113221.html)
