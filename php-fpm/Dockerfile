#
# MAINTAINER        Carson,C.J.Zeong <zcy@nicescale.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing Nginx: Dockerfile for building Nginx images
#
FROM       csphere/demobase:0.1
MAINTAINER Carson,C.J.Zeong <zcy@nicescale.com>

# Set environment variable
ENV HTML_DIR /app

# Install nginx server and php 
RUN	yum -y install nginx mysqli php-cli php php-mysql php-pear php-ldap php-mbstring php-soap php-dom php-gd php-xmlrpc php-fpm php-mcrypt && \ 
	yum clean all

# Config and install scripts
COPY material/setup /setup
RUN chmod +x /setup/install && \
	exec /setup/install

# Delete setup scripts after install
RUN rm -rf /setup

# Add start container scripts
COPY scripts /scripts
RUN chmod +x /scripts/start

EXPOSE 80 443

ENTRYPOINT ["/scripts/start"]

CMD ["runStart"]

ONBUILD ADD . /app