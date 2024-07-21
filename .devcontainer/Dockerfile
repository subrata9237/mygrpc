FROM arm64v8/ubuntu:20.04

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Install necessary packages
RUN apt-get update && apt-get install -y \
    build-essential \
    doxygen \
    graphviz \
    autoconf \
    libtool \
    pkg-config \
    cmake \
    git \
    curl \
    wget \
    unzip \
    gdb \
    clang \
    clang-format \
    lldb \
    python3 \
    python3-pip \
    nano

# Install Protocol Buffers
RUN git clone -b v3.14.0 https://github.com/protocolbuffers/protobuf.git \
    && cd protobuf \
    && git submodule update --init --recursive \
    && ./autogen.sh \
    && ./configure \
    && make -j$(nproc) \
    && make install \
    && ldconfig \
    && cd .. \
    && rm -rf protobuf

# Install gRPC
RUN git clone -b v1.35.0 https://github.com/grpc/grpc.git \
    && cd grpc \
    && git submodule update --init --recursive \
    && mkdir -p cmake/build \
    && cd cmake/build \
    && cmake ../.. \
    && make -j$(nproc) \
    && make install \
    && ldconfig \
    && cd ../../.. \
    && rm -rf grpc

# Set the working directory
WORKDIR /workspaces/

# Copy the current directory contents into the container
COPY . .
RUN ls -a
# Build the gRPC project
#RUN cmake -S . -B build \
 #   && cmake --build build

# Set environment variables for the binaries
ENV PATH="/workspace/build:${PATH}"

# Default command to run when the container starts
CMD ["bash"]