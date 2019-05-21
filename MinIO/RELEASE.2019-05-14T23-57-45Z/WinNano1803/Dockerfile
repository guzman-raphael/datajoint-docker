FROM mcr.microsoft.com/powershell:6.2.0-nanoserver-1803

MAINTAINER raphael.h.guzman@gmail.com

ENV MINIO_ACCESS_KEY datajoint
ENV MINIO_SECRET_KEY datajoint

WORKDIR C:/minio
RUN mkdir data
RUN pwsh -NoLogo -NoProfile -Command "Invoke-WebRequest -Uri https://dl.minio.io/server/minio/release/windows-amd64/minio.exe -OutFile minio.exe"

EXPOSE 9000
ENTRYPOINT [ "C:/minio/minio.exe" ]
CMD [ "server" , "--config-dir" , "config" , "data" ]
