FROM debian:stretch-slim

ENV PACKAGES "curl openssh-client file git openssl ca-certificates wget golang-1.8-go jq"

RUN apt-get update -y && \
  apt-get install -y $PACKAGES && \
  rm -rf /var/lib/apt/lists/*

RUN bash -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"

