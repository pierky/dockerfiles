FROM node:11

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install \
        -y \
        --no-install-recommends \
            curl \
            vim \
            make \
            git && \
    rm -rf /var/lib/apt/lists/*

ENV GOPATH="/root/go"
ENV PATH="${PATH}:/root/go/bin"

RUN curl -OL https://golang.org/dl/go1.15.6.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.15.6.linux-amd64.tar.gz

ENV PATH="${PATH}:/usr/local/go/bin"

RUN npm install --global gulp-cli@2.3.0
RUN npm install --global yarn@1.22.10

RUN GO111MODULE=on go get github.com/GeertJohan/go.rice@d954009f7238df62c766980934c8ea7f161d0e59
RUN GO111MODULE=on go get github.com/GeertJohan/go.rice/rice@d954009f7238df62c766980934c8ea7f161d0e59

RUN mkdir -p ~/go/bin ~/go/pkg ~/go/src/github.com/alice-lg/

RUN git clone https://github.com/alice-lg/alice-lg.git && \
    cd alice-lg && \
    git checkout d196c88e2959dcef2cdc05f24c74af4f83263a5d

RUN cd alice-lg && \
    make

RUN git clone https://github.com/alice-lg/alice-theme-example.git && \
    cd alice-theme-example && \
    git checkout c6587d1976fe530f9ff055288ff6b108c110beda

RUN mkdir /etc/alice-lg

COPY alice.conf /etc/alice-lg/

SHELL ["/bin/bash", "-c"]

CMD /alice-lg/bin/alice-lg-linux-amd64
