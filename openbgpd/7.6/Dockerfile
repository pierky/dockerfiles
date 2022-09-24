FROM debian:stable

MAINTAINER Pier Carlo Chiodi <pierky@pierky.com>

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

WORKDIR /root

# Using this specific commit since the one linked to the 7.6 release is
# not working due to some compile errors, which seem to be fixed here.
RUN curl -L https://github.com/openbgpd-portable/openbgpd-portable/archive/91fccddbe3d654f437f4ba0fe3691d14dd7f7960.zip -o 7.6.zip

RUN unzip 7.6.zip
RUN mv /root/openbgpd-portable-91fccddbe3d654f437f4ba0fe3691d14dd7f7960 /root/openbgpd-portable-7.6

RUN cd /root/openbgpd-portable-7.6 && \
    ./autogen.sh && \
    ./configure --sysconfdir=/etc/bgpd && \
    make && \
    make install

CMD /usr/local/sbin/bgpd -f /etc/bgpd/bgpd.conf -d
