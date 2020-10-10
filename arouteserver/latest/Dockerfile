FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install \
        -y \
        --no-install-recommends \
            vim \
            git \
            build-essential \
            python3-pip \
            python3-dev && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /bgpq3 && \
    cd /bgpq3 && \
    git clone https://github.com/snar/bgpq3.git ./ && \
    ./configure && \
    make && \
    make install

RUN pip3 install arouteserver

SHELL ["/bin/bash", "-c"]
