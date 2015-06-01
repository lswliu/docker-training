#
# MAINTAINER        Carson,C.J.Zeong <zcy@nicescale.com>
# DOCKER-VERSION    1.6.2
#
# Dockerizing Mariadb: Dockerfile for building Mariadb images
#
FROM csphere/demobase:0.1
MAINTAINER Carson,C.J.Zeong <zcy@nicescale.com>

# Set environment variables
ENV DATA_DIR /var/lib/mysql

# Install Mariadb
RUN yum install -y mariadb mariadb-server && \
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

EXPOSE 3306

VOLUME ["/var/lib/mysql"]

ENTRYPOINT ["/scripts/start"]

CMD ["runStart"]
