# docker build --build-arg DJ_VER=v0.12.dev4 .
ARG  PY_VER=3.7
ARG  ALPINE_VER=3.9
FROM python:${PY_VER}-alpine${ALPINE_VER}
ARG  DJ_VER=v0.12.dev4
MAINTAINER raphael.h.guzman@gmail.com

# min datajoint
RUN \
  apk update && \
  apk --no-cache --update-cache add --virtual build-min-dependencies \
    musl-dev g++ && \
  pip3 install pandas numpy networkx backcall

# diagram support
RUN \
  apk --no-cache --update-cache add --virtual build-erd-dependencies \
    pkgconfig && \
  apk --no-cache --update-cache add --virtual run-erd-dependencies \
    gcc freetype-dev graphviz ghostscript-fonts && \
  pip3 install matplotlib

# jupyter support
RUN \
  apk --no-cache --update-cache add --virtual build-jnb-dependencies \
    curl make && \
  mkdir -p min-package && \
  cd min-package && \
  curl -L https://archive.org/download/zeromq_4.0.4/zeromq-4.0.4.tar.gz > package.tar.gz && \
  tar -xzf package.tar.gz && \
  rm package.tar.gz && \
  cd $(ls) && \
  ./configure && make && make install && \
  cd ../../ && \
  rm -rf min-package && \
  strip --strip-unneeded --strip-debug /usr/local/lib/*.a || true && \
  strip --strip-unneeded --strip-debug /usr/local/lib/*.so* || true && \
  pip3 install jupyter

# remove build dependencies
RUN \
  apk del build-min-dependencies && \
  apk del build-erd-dependencies && \
  apk del build-jnb-dependencies

# Install DataJoint
RUN \
  apk --no-cache --update-cache add git && \
  mkdir /src && \
  cd /src && \
  git clone -b ${DJ_VER} --single-branch https://github.com/datajoint/datajoint-python.git && \
  cd datajoint-python && \
  pip install .  

CMD ["python","--version"]
