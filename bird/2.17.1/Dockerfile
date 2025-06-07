FROM debian:stable

ARG BIRD_VER=2.17.1

LABEL maintainer="Pier Carlo Chiodi <pierky@pierky.com>"

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

RUN curl -O -L https://bird.nic.cz/download/bird-${BIRD_VER}.tar.gz
RUN tar -zxvf bird-${BIRD_VER}.tar.gz

# This directory must be mounted as a local volume with '-v `pwd`/bird:/etc/bird:rw' docker's command line option.
# The host's file at `pwd`/bird/bird.conf is used as the configuration file for BIRD.
RUN mkdir /etc/bird

RUN cd bird-${BIRD_VER} && \
	autoconf && \
	autoheader && \
	./configure && \
	make && \
	make install

CMD bird -c /etc/bird/bird.conf -d
