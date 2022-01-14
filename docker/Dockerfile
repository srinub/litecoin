FROM ubuntu:18.04

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  curl ca-certificates

ARG LITECOIN_VERSION=0.18.1 

RUN useradd -ms /bin/false -u 1001 -U litecoin
USER litecoin
WORKDIR /home/litecoin/

RUN curl -fsSL https://download.litecoin.org/litecoin-$LITECOIN_VERSION/linux/litecoin-$LITECOIN_VERSION-x86_64-linux-gnu.tar.gz \ 
        -o litecoin.tar.gz && \
    curl -fsSL https://download.litecoin.org/litecoin-$LITECOIN_VERSION/linux/litecoin-$LITECOIN_VERSION-linux-signatures.asc | \
        grep litecoin-$LITECOIN_VERSION-x86_64-linux-gnu.tar.gz | \
    awk '{print $1, "litecoin.tar.gz"}' > sig.txt && \
    sha256sum -c --strict sig.txt && rm sig.txt && \
    tar -zxvf litecoin.tar.gz && \
    mv  litecoin-0.18.1 litecoin

CMD ./litecoin/bin/litecoind    