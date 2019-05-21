FROM mcr.microsoft.com/powershell:6.2.0-nanoserver-1803
MAINTAINER raphael.h.guzman@gmail.com

ENV MYSQL_ROOT_PASSWORD simple

ADD https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.22-winx64.zip mysql.zip

RUN pwsh -NoLogo -NoProfile -Command \
    Expand-Archive -Path c:\mysql.zip -DestinationPath C:\ ; \
    ren C:\mysql-5.7.22-winx64 C:\MySQL ; \
    New-Item -Path C:\MySQL\data -ItemType directory ; \
    C:\MySQL\bin\mysqld.exe --initialize --log_syslog=0
    
ENV MYSQL C:\\MySQL

EXPOSE 3306
ENTRYPOINT [ "C:/MySQL/bin/mysqld.exe" ]
CMD [ "--console" , "--skip-name-resolve", "--skip-grant-tables", "--log_syslog=0" ]
