FROM retrage/nabla-rumprun:latest

# get dependencies
WORKDIR /src
RUN apt update && apt install -y \
  git \
  gcc \
  make \
  wget \
  xz-utils \
  genisoimage

# build python3 in rumprun-packages
WORKDIR /src/rumprun
RUN git clone https://github.com/nabla-containers/rumprun-packages.git
WORKDIR rumprun-packages
ENV PYTHON_BUILD /src/rumprun/rumprun-packages/python3/build
RUN git checkout 687c6da \
  && cp config.mk.dist config.mk \
  && make -C python3 RUMPRUN_TOOLCHAIN_TUPLE=x86_64-rumprun-netbsd \
  && rumprun-bake solo5_spt $PYTHON_BUILD/python.nabla $PYTHON_BUILD/python
