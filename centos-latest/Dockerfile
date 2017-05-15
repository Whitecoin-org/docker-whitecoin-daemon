# XWC source GiT: https://github.com/Whitecoin-org/whitecoin
# XWC daemon Docker GiT: https://github.com/Whitecoin-org/docker-whitecoin-daemon

# Dockerfile for building and deploying an Whitecoin daemon.

FROM centos:latest

MAINTAINER oizopower <oizopower@whitecoin.info>

RUN yum -y install http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-9.noarch.rpm && \
    yum -y install autoconf automake gcc-c++ libdb4-cxx libdb4-cxx-devel boost-devel openssl-devel wget curl && \
    yum -y groupinstall "Development tools"

RUN cd /usr/src && wget https://www.openssl.org/source/openssl-1.0.2k.tar.gz && tar zxvf openssl-1.0.2k.tar.gz && \
    cd openssl-1.0.2k && export CFLAGS="-fPIC" && ./config --prefix=/usr --openssldir=/usr/local/openssl shared enable-ec enable-ecdh enable-ecdsa && \
    make all && make install

RUN git clone https://github.com/Whitecoin-org/whitecoin /node/whitecoinsource

WORKDIR /node/whitecoinsource/src

RUN wget -O /node/whitecoinsource/src/makefile-centos.unix https://raw.githubusercontent.com/Whitecoin-org/docker-whitecoin-daemon/master/centos-latest/makefile-centos.unix
RUN make -f makefile-centos.unix USE_UPNP=- && strip whitecoind && mv whitecoind /node/whitecoind && rm -rf /node/whitecoinsource

WORKDIR /node
VOLUME ["/node/home"]

ENV HOME /node/home

CMD ["/node/whitecoind"]

# PORT, RPCPORT
EXPOSE 15814 15815