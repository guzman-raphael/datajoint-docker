FROM alpine:3.9
MAINTAINER raphael.h.guzman@gmail.com

WORKDIR /app
VOLUME /app
COPY entrypoint.sh /entrypoint.sh

RUN apk add --update mysql mysql-client && rm -f /var/cache/apk/*
COPY my.cnf /etc/mysql/my.cnf

EXPOSE 3306
CMD ["/entrypoint.sh"]