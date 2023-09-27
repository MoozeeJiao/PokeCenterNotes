# Docker

> 参考链接：https://tech.meituan.com/2015/01/27/docker-introduction.html

## 简介

DotCloud开源，可以*将任何应用包装在Linux Container中运行的工具*。基于Doker提供的沙箱环境可以实现轻型隔离。

一组受限的进程（并没有真正的容器，只不过Docker在进程创建时加上了各种NS参数）：

* Cgroups：约束的主要手段，限制一个进程组能够使用的资源上限，包括CPU、内存、磁盘、网络。还能对进程进行优先级设置。
* Namespace：修改进程视图，如 PID、Mount、UTS、Network、User等资源都能修改进程所看到的视图。


### Docker vs VM

![[docker_vs_VM.png]]

VM是一个运行在宿主机上的完整操作系统，自身会占用较多的CPU、内存、硬盘资源。Docker只包含应用程序和依赖库，基于libcontainer运行在宿主机上，但是其隔离效果不如VM，共享宿主机操作系统的一些基础库。

Linux内核中，很多资源无法被NS隔离，最典型的就是时间。

## 组件

Docker 是CS架构

![[docker_comp.png]]

* Docker daemon: 运行在宿主机上，用户通过Docker Client与之交互；
* Docker client: 通过socker或api与Docker daemon进行通信；
* Docker hub/registry: 共享管理Docker镜像。

* Docker image: 镜像是只读的，其中包含需要运行的文件，镜像用来创建container，一个镜像可以运行多个container。*镜像可以通过Dockerfile创建*，也可以从Docker hub中下载。
* Docker container: 容器是Docker的运行组件，启动一个镜像就是启动容器，容器是一个隔离环境，多个容器间不会互相影响。

## Docker 网络

默认使用bridge桥接的方式与容器通信。

* bridge方式: 启动Docker后，会产生一个docker0的虚拟以太网桥。每次创建一个容器，都会产生一对虚拟接口绑定到docker0上。
* host方式: 容器直接使用宿主机网络接口。
* container方式: 让容器共享一个已存在的容器网络配置。
* none方式: 不对容器网络做任何配置，用户自己定制。



