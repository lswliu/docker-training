#
# MAINTAINER        Carson,C.J.Zeong <zcy@nicescale.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing CentOS7: Dockerfile for building CentOS images
#
FROM       centos:centos7.1.1503
MAINTAINER Carson,C.J.Zeong <zcy@nicescale.com>

# set environment variables
ENV TZ "Asia/Shanghai"

# ADD aliyun yum reop,Install packages, Supervisord
ADD material/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo
ADD material/epel.repo /etc/yum.repos.d/epel.repo

RUN yum update -y && \
    yum install -y curl wget tar bzip2 unzip vim-enhanced passwd sudo yum-utils hostname net-tools rsync man && \
    yum install -y gcc gcc-c++ git make automake cmake patch logrotate python-devel libpng-devel libjpeg-devel && \
    yum install -y --enablerepo=epel pwgen python-pip && \
    yum clean all

RUN pip install supervisor

# config and install scripts
COPY material/setup/ /setup

RUN chmod +x /setup/install && \
    exec /setup/install

# Delete setup scripts after install
RUN rm -fr /setup

EXPOSE 22

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]