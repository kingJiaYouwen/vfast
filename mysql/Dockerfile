#
# MAINTAINER        Jiayouwne<1962788818@qq.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing Mariadb: Dockerfile for building Mariadb images
#
FROM vfast/centos:7.1
MAINTAINER Jiayouwne<1962788818@qq.com>

ENV DATA_DIR /var/lib/mysql

# Install Mariadb
RUN yum install -y mariadb mariadb-server && \
    yum clean all

ADD mysqld_charset.cnf /etc/my.cnf.d/

COPY scripts /scripts
RUN chmod +x /scripts/start

EXPOSE 3306

VOLUME ["/var/lib/mysql"]
#这个地方重点说一下，这个就是我们数据持久化的方式了，

ENTRYPOINT ["/scripts/start"]


#在这个镜像构建的时候，你可以基于我们的php-from这个镜像来构建这个MySQLDB的镜像，也可以基于我们第一个镜像来做构建我选择centos而不选择php是因为一但我们PHP更新了以后我们的DB也是需要更新的，这样的话，就会有连锁反应。维护不方便。
#现在的话，就不会有一个升级全部都升级了。
