FROM itsafeaturemythic/mythic_base:latest

ARG RUST_VERSION=stable

ENV PATH="/root/.cargo/bin:${PATH}"

RUN apt-get -y update && \
    apt-get -y autoremove && \
    apt-get install --no-install-recommends  \
        build-essential \
        cmake \
        libxml2-dev \
        libssl-dev \
        git \
        curl \
        clang \
        gcc \
        g++ \
        zlib1g-dev \
        libmpc-dev \
        libmpfr-dev \
        libgmp-dev \
        mingw-w64 \
        nano \
        musl-tools -y && \
    rm -rf /var/lib/apt/lists/*

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

# Install tool chains
RUN /root/.cargo/bin/rustup toolchain install ${RUST_VERSION} && \
    /root/.cargo/bin/rustup component add rust-src --toolchain ${RUST_VERSION} && \
    /root/.cargo/bin/rustup target add --toolchain ${RUST_VERSION} \
    x86_64-apple-darwin \
    aarch64-apple-darwin \
    x86_64-unknown-linux-musl \
    aarch64-unknown-linux-musl \
    x86_64-pc-windows-gnu && \
    /root/.cargo/bin/rustup default ${RUST_VERSION}

# aarch64 specifics
RUN mkdir -p /build && cd /build && \
    curl -O https://musl.cc/aarch64-linux-musl-cross.tgz && \
    tar xvf aarch64-linux-musl-cross.tgz && \
    rm /build/aarch64-linux-musl-cross.tgz

ENV PATH="/build/aarch64-linux-musl-cross/bin:/build/osxcross/target/bin:${PATH}"