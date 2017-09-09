#
# MAINTAINER        Carson,C.J.Zeong <zcy@nicescale.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing CentOS7: Dockerfile for building CentOS images
#
FROM       centos:centos7.1.1503
#在咱们构建镜像的时候，首先得有一个基础的镜像，就是说，你现在要做的这个镜像的父镜像是谁。
MAINTAINER vfast.jia	<1962788818@qq.com>
#这个是作者，可有那可无的东西。维护者

ENV TZ "Asia/Shanghai"
#这个是我们当前设置的时区，也是一个环境变量，这个是可以写多个的。你像我们现在这个地方写的就是两个。
ENV TERM vfast


#这个我们add的指令，在我们的dockerfile中，有两条指令是可以copy文件的，第一个就是copy，第二个就是我们add指令，具体的不同之处请看博客。
#其实简单的说就是add比copy高级，因为，他多出来两个功能，直接解压copy。第二个就是copy。
ADD aliyun-mirror.repo /etc/yum.repos.d/CentOS-Base.repo
ADD aliyun-epel.repo /etc/yum.repos.d/epel.repo


#run指令，也就是一个镜像吧，这个里面的每一条命令都是可以拿到我们shell中执行的。别忘了，我们每一个指令就是一层，
RUN yum install -y curl wget tar bzip2 unzip vim-enhanced passwd sudo yum-utils hostname net-tools rsync man && \
    yum install -y gcc gcc-c++ git make automake cmake patch logrotate python-devel libpng-devel libjpeg-devel && \
    yum install -y --enablerepo=epel pwgen python-pip && \
    yum clean all

#因为我们现在要运行的是多个进程，这个是进程管理工具，方便我们管理进程。
RUN pip install supervisor
#这个是从我们容器的外面拷贝一个进程管理工具的配置文件，到我们容器的里面。
ADD supervisord.conf /etc/supervisord.conf

#这个是创建一个进程管理的目录，这个目录的里面存放的是我们管理其他进程的配置文件。
RUN mkdir -p /etc/supervisor.conf.d && \
#这个存放的是我们的日志目录。
    mkdir -p /var/log/supervisor

EXPOSE 22
#这个是我们暴露出来的端口号。

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
#最后的这个是我们启动运行时候的一个命令。
