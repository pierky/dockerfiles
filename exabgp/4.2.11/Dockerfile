FROM python:3.7

MAINTAINER Pier Carlo Chiodi <pierky@pierky.com>

EXPOSE 179

RUN apt-get update && apt-get install -y \
        unzip

WORKDIR /root
RUN curl -O -L https://github.com/Exa-Networks/exabgp/archive/refs/tags/4.2.11.zip
RUN unzip 4.2.11.zip

# This directory must be mounted as a local volume with '-v `pwd`/exabgp:/etc/exabgp:rw' docker's command line option.
# The host's file at `pwd`/exabgp/exabgp.conf is used as the configuration file for ExaBGP.
RUN mkdir /etc/exabgp

RUN mkdir -p /exabgp-4.2.11/etc/exabgp
ENV PATH /root/exabgp-4.2.11/bin:/root/exabgp-4.2.11/sbin:$PATH

RUN exabgp --fi > /root/exabgp-4.2.11/etc/exabgp/exabgp.env

CMD env exabgp.log.destination=/etc/exabgp/log exabgp.log.routes=true exabgp.daemon.user=root exabgp /etc/exabgp/exabgp.conf
