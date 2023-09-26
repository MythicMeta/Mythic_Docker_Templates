FROM python:3.11-slim-bookworm as base

ARG CA_CERTIFICATE
ARG NPM_REGISTRY
ARG PYPI_INDEX
ARG PYPI_INDEX_URL
ARG DOCKER_REGISTRY_MIRROR
ARG HTTP_PROXY
ARG HTTPS_PROXY

FROM base as builder

RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get install --no-install-recommends \
      software-properties-common apt-utils make build-essential libssl-dev zlib1g-dev libbz2-dev \
      xz-utils tk-dev libffi-dev liblzma-dev libsqlite3-dev protobuf-compiler \
      binutils-aarch64-linux-gnu libc-dev-arm64-cross -y  && \
    apt-get purge -y && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

RUN pip3 install mythic-container==0.2.11-rc07 pycryptodome

FROM base

COPY --from=builder /usr/local/lib/python3.11/ /usr/local/lib/python3.11/
