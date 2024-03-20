FROM debian:stable

LABEL maintainer="Pier Carlo Chiodi <pierky@pierky.com>"

EXPOSE 179

RUN apt-get update && apt-get install -y \
    autoconf \
    build-essential \
    curl \
    flex \
    git \
    libevent-dev \
    libreadline-dev \
    libncurses5-dev \
    libtool \
    m4 \
    unzip \
    byacc

RUN groupadd _bgpd && \
    useradd -g _bgpd -s /sbin/nologin -d /var/empty -c 'OpenBGPD daemon' _bgpd && \
    mkdir -p /var/empty && \
    chown 0 /var/empty && \
    chgrp 0 /var/empty && \
    chmod 0755 /var/empty

# This directory must be mounted as a local volume with '-v `pwd`/bgpd:/etc/bgpd:rw' docker's command line option.
# The host's file at `pwd`/bgpd/bgpd.conf is used as the configuration file for OpenBGPD.
RUN mkdir /etc/bgpd

ARG release=8.4

WORKDIR /root
RUN curl -L https://github.com/openbgpd-portable/openbgpd-portable/archive/${release}.zip -o ${release}.zip

RUN unzip ${release}.zip

# Fix from https://github.com/openbgpd-portable/openbgpd-portable/issues/75
RUN curl -L \
    https://github.com/openbgpd-portable/openbgpd-portable/commit/42da261565ae849fdaabf9813362d37f00446bbf.patch \
    -o /root/openbgpd-portable-${release}/fix.patch
RUN cd /root/openbgpd-portable-${release} && \
    patch -p 1 < fix.patch

RUN cd /root/openbgpd-portable-${release} && \
    ./autogen.sh && \
    ./configure --sysconfdir=/etc/bgpd && \
    make && \
    make install

CMD /usr/local/sbin/bgpd -f /etc/bgpd/bgpd.conf -d
