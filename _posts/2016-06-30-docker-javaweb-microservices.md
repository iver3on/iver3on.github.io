---
layout: post
title:  "win10下docker部署java web环境+挂载windows10目录+部署应用"
date:   2016-06-30 11:06:05
categories: 分布式
tags: docker 微服务 分布式 linux tomcat
---

* content
{:toc}

总结在win10下docker部署java web环境+挂载windows10目录+部署应用




## 部署环境
windows环境下在docker容器部署java web环境：

一般搭建环境需要自己编写dockerfile文件，类似下面：
> FROM dordoka/tomcat  
> MAINTAINER iver3on <grepzwb@qq.com> 
> ENV REFRESHED_AT 2016-6-28 
> EXPOSE 8080 9000</blockquote> 
> 但是docker官方给我们提供了太多了开源镜像，比如tomcat mysql jdk redis ruby 等。。。我们可以直接pull即可。 

所以我直接打开Docker Quickstart Terminal，登陆docker。

先象征性的docker search tomcat.看看镜像仓库都有tomcat相关的什么镜像：

<img class="aligncenter" src="http://7xui79.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160630184927.png" width="689" height="413" />

一般选择star多或者官方的镜像。

[tomcat官方镜像](https://hub.docker.com/_/tomcat/)

docker pull tomcat

然后docker image 查看本地仓库是不是出现了。

一般docker容器tomcat开放的是8080端口。在run的时候需要映射主机host的特定端口，这个host的windows环境下就是default虚拟机。
<blockquote>Docker 能够很容易的配置和绑定网络端口。在最后一个例子中 标识(flags)是 8080 的缩写，它将会把容器内部的 8080 端口映射到本地 Docker 主机的高位端口上(这个端口的通常范围是 32768 至 61000)。我们也可以指定标识来绑定指定端口8888。举例：</blockquote>
<span style="color: #ff0000;">docker run -it -p 8888:8080 -v /mnt/win10/:/opt/tomcat/webapp/ tomcat:8.0</span>

<span style="color: #ff0000;">这将会把容器内部的 8080 端口映射到我们本地主机的 8888 端口上。你可能现在会问：为什么我们只使用 1对1端口映射的方式将端口映射到 Docker 容器， 而不是采用自动映射高位端口的方式？这里 1:1 映射方式能够保证映射到本地主机端口的唯一性。假设你想要测试两个 Python 应用程序，两个容器内部都绑定了端口8888，这样就没有足够的 Docker 的端口映射，你只能访问其中一个。</span>

这样docker容器的web还将就配置好了。很简单。因为官方的镜像内部dockerfile文件已经将所需的jdk tomcat都写好了。想看这个文件可以在github查看：

[]("https://github.com/docker-library/tomcat/blob/8323df4824d3661f094a1a6c30ed7e13c0536b9e/8.0/jre8/Dockerfile">https://github.com/docker-library/tomcat/blob/8323df4824d3661f094a1a6c30ed7e13c0536b9e/8.0/jre8/Dockerfile)
## 挂载目录
因为开发一般是在windows环境下开发的，但是docker必须在linux环境下才可以运行。所以windows下面必须使用虚拟机。如此，需要将windows下面的目录挂载到虚拟机，由虚拟机在挂载到容器的目录下面，比如容器的tomcat/webapps/下面。这样开发后的war文件就可以直接在容器里使用。
### 建立virtualbox和docker虚拟主机default的共享
点击共享文件夹设置框，右上角的添加按钮

![]("http://f.hiphotos.baidu.com/exp/w=480/sign=107cd686ad51f3dec3b2b86ca4eff0ec/241f95cad1c8a786447d54426509c93d70cf5022.jpg" width="540" height="450")

选择之前本机设置的共享文件夹，此时一定不可以勾选自动挂载

![xx]("http://7xui79.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160630192055.png" width="628" height="381")

设置好共享名后，进入docker虚拟机系统，打开终端，先执行命令，在挂载点目录添加“win10”目录，接着执行"mount -t vboxsf warjar /mnt/win10/",就能完成共享文件夹的设置。请记住mount命令一定要带上参数-t vboxsf，warjar就是windows10下共享文件夹名称，/mnt/win10/就是要在docker虚拟机中挂载的绝对路径
docker虚拟机系统默认使用docker用户，可能会遇到Permission denied错误，即权限不足，需要切换到root账户操作，只要输入“sudo su”命令即可，无需密码
### docker容器挂载docker虚拟机的目录
docker可以支持把一个宿主机上的目录挂载到镜像里。

docker run -it -p 8888:8080 -v /mnt/win10/:/opt/tomcat/webapp/ tomcat:8.0
通过-v参数，冒号前为宿主机目录，必须为绝对路径，冒号后为镜像内挂载的路径。

现在镜像内就可以共享宿主机里的文件了。
这样就把宿主windows的E:\warjar目录，挂载到了container的/opt/tomcat/webapp/目录 

两个目录即可共享。写完项目。打包后直接将war放到E:\warjar。也就相当于放到了container的/opt/tomcat/webapp/。
## 打包应用在docker执行 
在window上写好web应用或者spring boot应用。下一步打包为war。然后将war放到E:\warjar。也就相当于放到了container。使用default虚拟主机的IP地址访问映射的8080端口如下：

docker run -it -p 8080:8080 -v /mnt/win10/:/opt/tomcat/webapp/ tomcat:8.0

![]("http://7xui79.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160630184100.png" width="698" height="204")

Ok.部署完成。后续可以将每个微服务打包为jar或者war部署在docker实现进程式管理。实现微服务部署。 
