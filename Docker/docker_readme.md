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
* 查看本地镜像 `docker images`
* 移除镜像 `docker rmi image_name`
* 后台运行容器 `docker run -d image_name`
* 通过交互式的方式运行容器 `docker run -it image_name`
* 修改镜像名称 `docker tag dl.dockerpool.com:5000/ubuntu:12.04 ubuntu:12.04`

## 容器
### 概念
Docker容器（Container）类似于一个轻量级的沙箱，Docker利用容器来运行和隔离应用。
容器是从镜像创建的应用运行实例，可以将其启动、开始、停止、删除，而这些容器都是相互隔离、互不可见的。
可以把容器看做一个简易版的Linux系统环境（这包括root用户权限、进程空间、用户空间和网络空间等），以及运行在其中的应用程序打包而成的应用盒子。
镜像自身是 **只读** 的。容器从镜像启动的时候，Docker会在镜像的最上层创建一个 **可写** 层，镜像本身将保持不变。  
### 基本指令
* 列出正在运行的容器 `docker ps`
* 列出所有的容器 `docker ps -a`
* 创建容器 `docker create -it ubuntu:latest`
* 创建并运行容器 `docker run ubuntu  /bin/echo 'Hello world'`
* 停止正在运行的容器 `docker stop image_id`
* 启动容器 `docker start image_id`
* 重启容器 `docker restart image_id`
* attach容器 `docker attach image_name`
* 删除容器 `docker rm image_name`
* 强制删除容器 `docker rm -f image_name`
* 导出容器 `docker export iamge_id >file_name.tar`
* 导入容器 `cat file_name.tar | sudo docker import - image_name:tag`

## 仓库
### 概念
熟悉Git和GitHub的同学，可以很容易的理解镜像和仓库的概念。而最著名的镜像仓库就是DockerHub。
前面所说的操作`docker pull`和`docker search`其实都是本地机器向远端的服务器进行查询和拉取。默认的服务器为DockerHub。由于国内使用Docker下载各种镜像速度较慢，所以需要借助一些国内的镜像进行 **加速** :  
[DaoCloud 加速器地址（需要注册账号）](https://www.daocloud.io/mirror#accelerator-doc)

### 基本指令
* 查询镜像 `docker search image_name`
* 获取镜像 `docker pull image_name`
* 推送镜像 `docker push image_name`

## 数据管理
### 概念
数据卷是一个可供容器使用的特殊目录，它绕过文件系统，可以提供很多有用的特性。数据卷的使用，类似于Linux下对目录或文件进行mount操作。

### 基本指令
* 在容器内创建一个数据卷 `docker run -it -v /my_dir ubuntu /bin/bash`
* 挂载一个主机目录或文件作为数据卷 `docker run -it -v /host_dir:/my_dir ubuntu /bin/bash` 将本地主机`/host_dir`挂在到了容器中的`/my_dir`中。注意需要使用绝对路径


## 其他指令
* 显示容器的标准输出 `docker logs image_id`

---
**参考资料**
* [Docker 加速器](http://guide.daocloud.io/dcs/daocloud-9153151.html#docker-toolbox)
* [在Windows中玩转Docker Toolbox](http://www.cnblogs.com/studyzy/p/6113221.html)
