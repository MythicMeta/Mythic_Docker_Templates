FROM itsafeaturemythic/mythic_base:latest

ARG CA_CERTIFICATE
ARG NPM_REGISTRY
ARG PYPI_INDEX
ARG PYPI_INDEX_URL
ARG DOCKER_REGISTRY_MIRROR
ARG HTTP_PROXY
ARG HTTPS_PROXY

# install .net core
RUN wget https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    rm packages-microsoft-prod.deb

# install mono, protoc protobufs, and .net core 
RUN apt-get -y update && \
    apt-get -y autoremove && \
    apt-get clean && \
    apt-get install --no-install-recommends llvm libncurses5-dev libncursesw5-dev gcc-mingw-w64 -y && \
    rm -rf /var/lib/apt/lists/*

#
# allow cross compilation for macOS
# Configure the container for OSX cross compilation
RUN ln -s /usr/include/asm-generic /usr/include/asm

RUN bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"
RUN apt-get install --no-install-recommends clang-15 clang-15++ cmake -y
RUN ln -s /usr/bin/clang-15 /usr/bin/clang
RUN ln -s /usr/bin/clang++-15 /usr/bin/clang++
ENV OSX_SDK 12.1
RUN cd / && git clone --depth 1 https://github.com/tpoechtrager/osxcross.git && \
  cd osxcross && curl -fsSL -O https://github.com/joseluisq/macosx-sdks/releases/download/${OSX_SDK}/MacOSX${OSX_SDK}.sdk.tar.xz && \
  mv MacOSX${OSX_SDK}.sdk.tar.xz tarballs/ && UNATTENDED=yes ./build.sh && rm -rf  /build/osxcross/tarballs/

ENV PATH /osxcross/target/bin:$PATH
ENV LD_LIBRARY_PATH=/osxcross/target/lib