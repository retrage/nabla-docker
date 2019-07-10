FROM ubuntu:bionic

# get dependencies
WORKDIR /src
RUN apt update && apt install -y \
  git \
  gcc \
  make \
  libseccomp-dev \
  zlib1g-dev

# build solo5 rumprun
RUN git clone https://github.com/nabla-containers/rumprun.git
WORKDIR rumprun
COPY patches/0001-Avoid-gcc-warning-error.patch .
RUN git checkout 4ddcdd2 \
  && git apply 0001-Avoid-gcc-warning-error.patch \
  && git submodule init \
  && git submodule update \
  && make build
ENV PATH /src/rumprun/rumprun-solo5/bin:$PATH
