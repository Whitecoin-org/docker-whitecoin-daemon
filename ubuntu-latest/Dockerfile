# XWC source GiT: https://github.com/Whitecoin-org/whitecoin
# XWC daemon Docker GiT: https://github.com/Whitecoin-org/docker-whitecoin-daemon

# Dockerfile for building and deploying an Whitecoin daemon.

FROM ubuntu:latest

MAINTAINER oizopower <oizopower@whitecoin.info>

RUN apt-get install --yes software-properties-common && \
    add-apt-repository --yes ppa:bitcoin/bitcoin && \
    apt-get update --yes && apt-get install --yes \
       autoconf \
       automake \
       autotools-dev \
       bsdmainutils \
       build-essential \
       git \
       libboost-all-dev \
       libboost-filesystem-dev \
       libboost-program-options-dev \
       libboost-system-dev \
       libboost-test-dev \
       libboost-thread-dev \
       libdb4.8++-dev \
       libdb4.8-dev \
       libevent-dev \
       libminiupnpc-dev \
       libprotobuf-dev \
       libqrencode-dev \
       libqt5core5a \
       libqt5dbus5 \
       libqt5gui5 \
       libqt5webkit5-dev  \
       libsqlite3-dev \
       libssl-dev \
       libtool \
       pkg-config \
       protobuf-compiler \
       qt5-default \
       qtbase5-dev \
       qtdeclarative5-dev \
       qttools5-dev \
       qttools5-dev-tools

RUN git clone https://github.com/Whitecoin-org/whitecoin /node/whitecoinsource

WORKDIR /node/whitecoinsource/src

RUN makefile -f makefile.unix USE_UPNP=- && strip whitecoind && mv whitecoind /node/whitecoind && rm -rf /node/whitecoinsource

WORKDIR /node
VOLUME ["/node/home"]

ENV HOME /node/home

CMD ["/node/whitecoind"]

# PORT, RPCPORT
EXPOSE 15814 15815