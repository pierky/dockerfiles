FROM pierky/quagga:1.1.1

MAINTAINER Pier Carlo Chiodi <pierky@pierky.com>

EXPOSE 179

RUN apt-get update && apt-get install -y libz-dev libbz2-dev

WORKDIR /root
RUN curl -o bgpdump2-master.zip -L https://github.com/yasuhiro-ohara-ntt/bgpdump2/archive/master.zip
RUN unzip bgpdump2-master.zip

RUN cd bgpdump2-master && \
	./configure && \
	make && \
	make install
