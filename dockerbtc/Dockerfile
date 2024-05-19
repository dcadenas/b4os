FROM --platform=linux/arm64/v8 arm64v8/ubuntu AS base

WORKDIR /root

RUN apt-get update && apt-get install -y wget vim bash-completion jq git autoconf libtool g++ pkg-config make libreadline-dev
ARG BITCOIN_CORE_HASH="cb35e250ae9d0328aa90e7aad0b877ed692597420a1092e8ab1a5dd756209722  bitcoin-27.0-aarch64-linux-gnu.tar.gz"
RUN wget https://bitcoincore.org/bin/bitcoin-core-27.0/bitcoin-27.0-aarch64-linux-gnu.tar.gz
RUN echo $BITCOIN_CORE_HASH | sha256sum -c -
RUN tar -xvf bitcoin-27.0-aarch64-linux-gnu.tar.gz
ENV PATH="/root/bitcoin-27.0/bin:${PATH}"

WORKDIR /tmp/

RUN apt-get update && apt-get install -y bash-completion
RUN mkdir -p /etc/bash_completion.d/ && \
    wget https://raw.githubusercontent.com/bitcoin/bitcoin/master/contrib/completions/bash/bitcoind.bash && \
    wget https://raw.githubusercontent.com/bitcoin/bitcoin/master/contrib/completions/bash/bitcoin-cli.bash && \
    wget https://raw.githubusercontent.com/lightningnetwork/lnd/master/contrib/lncli.bash-completion && \
    mv bitcoind.bash bitcoin-cli.bash lncli.bash-completion /etc/bash_completion.d/


RUN git clone https://github.com/bitcoin-core/btcdeb.git
WORKDIR /tmp/btcdeb
RUN ./autogen.sh && ./configure && make && make install

WORKDIR /root/exercises
COPY bashrc /root/.bashrc

CMD tail -f /dev/null
