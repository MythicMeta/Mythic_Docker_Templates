FROM itsafeaturemythic/mythic_go_base:latest

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
RUN apt-get install --no-install-recommends clang-17 clang-17++ cmake -y
RUN ln -s /usr/bin/clang-17 /usr/bin/clang
RUN ln -s /usr/bin/clang++-17 /usr/bin/clang++
ENV OSX_SDK 12.1
RUN cd / && git clone --depth 1 https://github.com/tpoechtrager/osxcross.git && \
  cd osxcross && curl -fsSL -O https://github.com/joseluisq/macosx-sdks/releases/download/${OSX_SDK}/MacOSX${OSX_SDK}.sdk.tar.xz && \
  mv MacOSX${OSX_SDK}.sdk.tar.xz tarballs/ && UNATTENDED=yes ./build.sh && rm -rf  /build/osxcross/tarballs/

ENV PATH /osxcross/target/bin:$PATH
ENV LD_LIBRARY_PATH=/osxcross/target/lib