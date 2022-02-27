## Docker学习

> ##### 环境配置特别麻烦, 尤其是每个机器上都要部署时
>

​	传统: 项目打包文件交给运维人员来做
​	现在: 开发打包部署上线

###### 总结一下就是将项目和环境一起打包

## Docker能做什么

> ###### 之前的虚拟机技术

###### 要部署一整个操作系统, 同时运行多个程序

- ###### 	缺点

  - 资源占用多
  - 冗余步骤多
  - 启动很慢

![image-20220220143125594](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220220143125594.png)

> ###### 容器化技术
###### 容器化技术不是模拟的一个完整的操作系统
###### 更快速的交互和部署
![image-20220220143559104](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220220143559104.png)

###### Docker与传统虚拟机的不同

- ###### 传统虚拟机, 虚拟出一套硬件, 运行一个完整的操作系统, 然后在这个系统上安装和运行软件

- ###### 容器内的应用直接运行再宿主机的内容, 容器是没有自己的内核的, 也没有虚拟硬件, 所以就轻便了

  - 每个容器间是互相隔离的. 每个容器内有一个属于自己的文件系统, 互不影响

> ###### DevOps(开发, 运维)

###### 应用更快速的交付和部署

- 传统: 一堆帮助文档, 安装程序
- Docker: 打包镜像发布测试, 一键运行

###### 更便捷的升级和扩缩容

- 使用了Docker后, 部署应用就像搭积木一样
- 直接将项目打包成一个镜像, 扩展时直接运行新的镜像

###### 更简单的系统运维

- 在容器化之后, 我们的开发, 测试环境都是高度一致的

###### 更高效的计算资源利用

- Docker时内核级别的虚拟化, 可以在一个机器上运行很多的容器实例, 服务器的性能可以被发挥到极致

# **Docker安装**

#### Docker的基本组成

![image-20220220145343164](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220220145343164.png)

###### 镜像(image)

- 镜像就好比一个类, 可以通过这个类来创建实例(容器服务)

###### 容器(container)

- Docker利用容器技术, 独立运行一个或一组应用, 通过镜像来创建的
- 启动, 停止, 删除等基本命令

###### 仓库(repository)

- 仓库就是存放镜像的地方, 和GitHub的仓库一个概念
- 分为公有和私有仓库

#### 安装Docker

> ###### 环境准备

1. 需要一点linux基础
2. CentOS 7
3. 使用Xshell连接远程服务器

> ###### 环境查看

```shell
root@LAPTOP-71VL09VG:/mnt/d# uname -r
5.10.60.1-microsoft-standard-WSL2
root@LAPTOP-71VL09VG:/mnt/d#
```

```shell
root@LAPTOP-71VL09VG:/mnt/d# cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
root@LAPTOP-71VL09VG:/mnt/d#
```

> ###### 安装

[Docker-Linux官方安装教程](https://docs.docker.com/engine/)

###### 安装完成后输入`docker version`查看版本, 不报错表示安装成功

![image-20220220160244418](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220220160244418.png)

###### 可以在Windows商店中安装Ubuntu, 并安装WSL

[Windows安装Linux环境(WSL)](https://blog.csdn.net/weixin_52802958/article/details/122631592)

###### *在Windows上操作需要同时运行Docker Desktop*

`docker images` 查看镜像

> 镜像运行流程

`docker run hello-world`

- ###### 首先会在本机寻找镜像

  - 如果有这个镜像则会运行
  - 如果没有这个镜像, 则会去DockerHub中下载
    - 如果找不到则会返回错误: 找不到镜像
    - 如果找到了则下载镜像到本地并运行

# **镜像的基本命令**

##### 帮助命令

```
docker version	--版本信息
docker info 	--x
docker --help	--万能命令
```

##### 新建容器并使用

```shell
docker run [可选参数] image
# 参数说明
--name="Name"	容器名称 name1, name2 用来区分容器
-d				后台方式运行
-it				使用交互的方式运行, 进入容器查看内容
-p				指定容器的端口
	-p	主机端口: 容器端口(常用)
	-p	容器端口
	-p	随机指定端口
	

```

```shell
docker pull centos #下载镜像
docker run -it centos /bin/bash	#启动centos

root@LAPTOP-71VL09VG:/mnt/d docker run -it centos /bin/bash
[root@c6d9d8529890 /]	#此处发生了变化, 说明我们进入了centos

[root@c6d9d8529890 /]# ls
bin  etc   lib    lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr

#从容器中退回主机: exit
```

##### 列出所有的运行的容器

```shell
docker ps	#列出当前运行中的容器
docker ps -a	#列出历史运行过的容器
docker ps -n=?	#列出最近创建的容器
docker ps -aq	#列出历史运行过的容器ID
```

##### 退出容器

```shell
exit	#直接退出容器并停止
Ctrl + P + Q	#容器不停止退出(后台运行)
```

##### 删除容器

```shell
docker rm 容器ID
docker rm -f 容器ID || 
$(docker ps -aq) || $(docker ps -a -q| ID1, ID2, ID3)
# '|' 管道符

#	不能删除当前正在运行的容器
root@LAPTOP-71VL09VG:/mnt/d# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS          PORTS     NAMES
f182af1dd6ac   centos    "/bin/bash"   11 seconds ago   Up 11 seconds             competent_almeida
root@LAPTOP-71VL09VG:/mnt/d# docker rm f182af1dd6ac
Error response from daemon: You cannot remove a running container f182af1dd6ac21d8ee34338349ed114e23e92df8cee9fc2cb4b808a4aff55449. Stop the container before attempting removal or force remove

#	增加-f并指定ID后, 可删除
root@LAPTOP-71VL09VG:/mnt/d# docker rm -f $(docker ps -aq)
```

##### 启动和停止容器的操作

```shell
docker start ID		#启动容器
docker restart ID	#重启容器
docker stop ID		#停止当前正在运行的容器
docker kill ID		#强制停止当前的容器
```



### 作业练习

> ##### 1. Docker安装Nginx

```shell
#搜索镜像 search 名称	#建议到dockerhub中搜索, 提供帮助文档
#下载镜像 pull
#运行测试
 #查看一下当前的镜像
root@LAPTOP-71VL09VG:/mnt/d# docker images
REPOSITORY               TAG       IMAGE ID       CREATED        SIZE
docker/getting-started   latest    bd9a9f733898   2 weeks ago    28.8MB
nginx                    latest    c316d5a335a5   4 weeks ago    142MB
mysql/mysql-server       latest    434c35b82b08   5 weeks ago    417MB
hello-world              latest    feb5d9fea6a5   5 months ago   13.3kB
centos                   latest    5d0da3dc9764   5 months ago   231MB
#	-d 后台运行
#	--name 容器命名
#	-p	主机端口: 容器端口
#启动nginx
root@LAPTOP-71VL09VG:/mnt/d# docker run -d --name nginx_test -p 3101:80 nginx
1173236234d6a79f7256aac779d28ab534619713e5f71e24811bc605f8cfcf56
#访问localhost:3101
root@LAPTOP-71VL09VG:/mnt/d# curl localhost:3101

```

> ##### 2.Docker安装tomcat

```shell
docker run -it --rm tomcat	#--rm表示容器停止时自动销毁容器, 常用于测试
docker run -it --name tomcat_test -p 3102:8080 tomcat	#运行tomcat
#运行后访问 会报404, 因为当前暂时没有webapps中暂未部署项目
#我们需要将webapps.dist的内容复制到webapps中
cp -r webapps.dist/* webapps
root@2f9841c7c453:/usr/local/tomcat/webapps# ls
ROOT  docs  examples  host-manager  manager
#有内容则表示复制成功了
```

![image-20220227153305885](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220227153305885.png)![image-20220227154025842](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220227154025842.png![image-20220227154044033](C:\Users\zhuoyue\AppData\Roaming\Typora\typora-user-images\image-20220227154044033.png)

> ##### 问题: 每次部署项目都需要进入容器, 非常麻烦, 有什么办法可以提高效率呢?
