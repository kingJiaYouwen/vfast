#
# MAINTAINER        Carson,C.J.Zeong <zcy@nicescale.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing php-fpm: Dockerfile for building php-fpm images
#
FROM       vfast/centos:7.1
MAINTAINER Jiayouwen <1962788818@qq.com>

# Set environment variable
ENV	APP_DIR /app
#这个修改的是我们Nginx的根目录。下面的ADD，大家可以看到我把那个默认的文件给覆盖掉了，

RUN     yum -y swap -- remove fakesystemd -- install systemd systemd-libs && \
        yum -y install nginx php-cli php-mysql php-pear php-ldap php-mbstring php-soap php-dom php-gd php-xmlrpc php-fpm php-mcrypt && \ 
	yum clean all

ADD nginx_nginx.conf /etc/nginx/nginx.conf
ADD	nginx_default.conf /etc/nginx/conf.d/default.conf

ADD	php_www.conf /etc/php-fpm.d/www.conf
RUN	sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/php.ini

RUN	mkdir -p /app && echo "<?php phpinfo(); ?>" > ${APP_DIR}/info.php
#这个是因为我们上边只是对这个目录进行了设置，我们还没有创建这个目录，这个地方的话我们创建一下这个目录。中间红色的部分是用来进行测试的，测试我们php-from和我们的Nginx链接是否成功。所以我们创建了一个info.php放到了我们刚才创建的这个目录的下边。

EXPOSE	80 443
#我们把容器的80,http和443，https这两个端口暴露出来。这个地方可以不写，但是考虑到团队协作，以及逻辑性，还是建议大家写上。

ADD	supervisor_nginx.conf /etc/supervisor.conf.d/nginx.conf
ADD	supervisor_php-fpm.conf /etc/supervisor.conf.d/php-fpm.conf
#添加我们Nginx和php-from的配置文件

ONBUILD ADD . /app
ONBUILD RUN chown -R nginx:nginx /app
#onbuild  这个货是干什么的呢？
#这个对于我们后期的测试，以及构建自动化的发布平台是至关重要的。
#现在的这个onbuild命令是不生效的，他什么时候生效呢？是在我们构建基于他的镜像的时候太才会生效。也就是说，我们from   这个镜像，onbuild是在下个镜像里生效的。
#这个命令用好的话，发布产品是非常快的。
