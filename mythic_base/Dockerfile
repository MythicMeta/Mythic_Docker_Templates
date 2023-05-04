FROM golang:1.20-buster

ARG CA_CERTIFICATE
ARG NPM_REGISTRY
ARG PYPI_INDEX
ARG PYPI_INDEX_URL
ARG DOCKER_REGISTRY_MIRROR
ARG HTTP_PROXY
ARG HTTPS_PROXY

RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get install --no-install-recommends \
      software-properties-common apt-utils make build-essential libssl-dev zlib1g-dev libbz2-dev \
      xz-utils tk-dev libffi-dev liblzma-dev libsqlite3-dev protobuf-compiler -y  && \
    apt-get purge -y && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

# install python 3.11
RUN wget https://www.python.org/ftp/python/3.11.1/Python-3.11.1.tgz && \
    tar xvf Python-3.11.1.tgz && \
    Python-3.11.1/configure --with-ensurepip=install && \
    make -j8 && \
    make install && \
    make clean

RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest && \
    go install google.golang.org/protobuf/cmd/protoc-gen-go@latest && \
    go install mvdan.cc/garble@latest

COPY requirements.txt /
RUN pip3 install -r /requirements.txt