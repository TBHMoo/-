## docker 是什么
Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

### 概念
* 容器  应用载体 可移植
* linux 环境
* 虚拟化 ？
* 容器使用沙箱模式，相互之间不会有任何接口 
* 性能开销低

### 安装
安装目录下执行 

$ brew cask install docker
[安装docker](http://www.runoob.com/docker/macos-docker-install.html)


xlidocker415
docker12345

lixiang
Yit123456

## docker hello world

```
$ docker run ubuntu:15.10 /bin/echo "hello"
```
#### 参数解析
* docker: Docker 的二进制执行文件。
* run:与前面的 docker 组合来运行一个容器。
* ubuntu:15.10指定要运行的镜像，Docker首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 Docker Hub 下载公共镜像。
* /bin/echo "Hello world": 在启动的容器里执行的命令

命令解释为，docker 以ubuntu:15.10 为镜像创建一个容器，然后在容器内执行 /bin/echo "hello" ，然后输出结果


## 运行交互式的容器
我们通过docker的两个参数 -i -t，让docker运行的容器实现"对话"的能力

```java_holder_method_tree
$ docker run -i -t ubuntu:15.10 /bin/bash
```
#### 参数解析
* -t:在新容器内指定一个伪终端或终端。

* -i:允许你对容器内的标准输入 (STDIN) 进行交互。

我们可以通过运行exit命令或者使用CTRL+D来退出容器。


## 启动容器（后台模式）
使用以下命令创建一个以进程方式运行的容器
```java_holder_method_tree
localhost:php_client xli$ docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
053da8ea7fdba6ec3052996431502fd6e49c59c8437b3f42582bc59910dda977
localhost:php_client xli$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
053da8ea7fdb        ubuntu:15.10        "/bin/sh -c 'while t…"   18 seconds ago      Up 17 seconds                           adoring_hofstadter
localhost:php_client xli$ docker logs 053da8ea7fdb
hello world
hello world
hello world
hello world
hello world
hello world
hello world
hello world
localhost:php_client xli$ docker stop 053da8ea7fdb
053da8ea7fdb
localhost:php_client xli$ 
```
返回的是后台运行的 容器id

```java_holder_method_tree
localhost:php_client xli$ docker
localhost:php_client xli$ docker stats --help
```

