MAINTAINER raphael.h.guzman@gmail.com
FROM stefanscherer/netapi-helper:1803 as core
FROM mcr.microsoft.com/powershell:6.2.0-nanoserver-1803
COPY --from=core /windows/system32/netapi32.dll /windows/system32/netapi32.dll

MAINTAINER raphael.h.guzman@gmail.com

ENV MINIO_ACCESS_KEY datajoint
ENV MINIO_SECRET_KEY datajoint

WORKDIR C:/minio-mc
RUN pwsh -NoLogo -NoProfile -Command "Invoke-WebRequest -Uri https://dl.minio.io/client/mc/release/windows-amd64/mc.exe -OutFile mc.exe"

RUN setx path "%path%;C:\minio-mc"

ENTRYPOINT ["pwsh.exe" , "-NoLogo", "-NoProfile", "-Command"]
CMD ["mc config host add dj-s3 http://minio:9000 datajoint datajoint;mc mb dj-s3/datajoint-test;mc policy download dj-s3/datajoint-test;while ($true) { start-sleep -seconds 60}"]
