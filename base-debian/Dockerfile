FROM debian:sid-slim

ENV PACKAGES "curl openssh-client file git openssl ca-certificates wget golang-1.11-go jq unzip python3-minimal python3-requests"

RUN apt-get update -y && \
  apt-get install -y $PACKAGES && \
  rm -rf /var/lib/apt/lists/*

RUN bash -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"

