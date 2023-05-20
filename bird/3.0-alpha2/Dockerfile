FROM debian:stable

MAINTAINER Pier Carlo Chiodi <pierky@pierky.com>

EXPOSE 179

RUN apt-get update && apt-get install -y \
    autoconf \
	bison \
	build-essential \
	curl \
	flex \
	libreadline-dev \
	libncurses5-dev \
	m4 \
	unzip

WORKDIR /root
RUN curl -O -L ftp://bird.network.cz/pub/bird/3.0pre/bird-3.0alpha2.tar.gz
RUN curl -O -L ftp://bird.network.cz/pub/bird/3.0pre/bird-doc-3.0alpha2.tar.gz

RUN tar -zxvf bird-3.0alpha2.tar.gz
RUN tar -zxvf bird-doc-3.0alpha2.tar.gz

# This directory must be mounted as a local volume with '-v `pwd`/bird:/etc/bird:rw' docker's command line option.
# The host's file at `pwd`/bird/bird.conf is used as the configuration file for BIRD.
RUN mkdir /etc/bird

RUN cd bird-3.0alpha2 && \
	autoconf && \
	autoheader && \
	./configure && \
	make && \
	make install

CMD bird -c /etc/bird/bird.conf -d
