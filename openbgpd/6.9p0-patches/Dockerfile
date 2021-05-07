FROM debian:stable

MAINTAINER Pier Carlo Chiodi <pierky@pierky.com>

EXPOSE 179

RUN apt-get update && apt-get install -y \
    autoconf \
    build-essential \
    curl \
    flex \
    git \
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
RUN curl -L https://github.com/openbgpd-portable/openbgpd-portable/archive/6.9p0.zip -o 6.9p0.zip

RUN unzip 6.9p0.zip

COPY *.patch /root/

RUN cd /root/openbgpd-portable-6.9p0 && \
    ./autogen.sh && \
    ./configure --sysconfdir=/etc/bgpd && \
    cd src/bgpd/ && \
    patch -l < /root/issue23-rtr.patch && \
    patch -l < /root/issue21-rde_evaluate_all_withdrawal.patch && \
    patch -l < /root/issue21-rde_evaluate_all_reload.patch && \
    patch -l < /root/rtr-non-blocking-connect.patch && \
    cd ../../ && \
    make && \
    make install

CMD /usr/local/sbin/bgpd -f /etc/bgpd/bgpd.conf -d
