FROM --platform=linux/arm64/v8 arm64v8/ubuntu AS base

WORKDIR /root

RUN apt-get update && apt-get install -y wget
ARG BITCOIN_CORE_HASH="cb35e250ae9d0328aa90e7aad0b877ed692597420a1092e8ab1a5dd756209722  bitcoin-27.0-aarch64-linux-gnu.tar.gz"
RUN wget https://bitcoincore.org/bin/bitcoin-core-27.0/bitcoin-27.0-aarch64-linux-gnu.tar.gz
RUN echo $BITCOIN_CORE_HASH | sha256sum -c -
RUN tar -xvf bitcoin-27.0-aarch64-linux-gnu.tar.gz
COPY bashrc /root/.bashrc
ENV PATH="/root/bitcoin-27.0/bin:${PATH}"

CMD ["bitcoind","-datadir=/root/.bitcoin", "-printtoconsole"]
