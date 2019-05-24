FROM alpine:3.9
MAINTAINER raphael.h.guzman@gmail.com

WORKDIR /app
VOLUME /app
COPY entrypoint.sh /entrypoint.sh

RUN apk add --update mysql mysql-client && rm -f /var/cache/apk/*
COPY my.cnf /etc/mysql/my.cnf

EXPOSE 3306
CMD ["/entrypoint.sh"]

https://dev.mysql.com/get/Downloads/MySQL-5.6/mysql-5.6.44.tar.gz
https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.22.tar.gz
https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.16.tar.gz


# Preconfiguration setup
addgroup mysql
useradd -G mysql -s /bin/false mysql
# Beginning of source-build specific instructions
tar zxvf mysql-VERSION.tar.gz
cd mysql-VERSION
./configure --prefix=/usr/local/mysql
make
make install
# End of source-build specific instructions
# Postinstallation setup
cd /usr/local/mysql
chown -R mysql .
chgrp -R mysql .
bin/mysql_install_db --user=mysql
chown -R root .
chown -R mysql var
# Next command is optional
cp support-files/my-medium.cnf /etc/my.cnf
bin/mysqld_safe --user=mysql &