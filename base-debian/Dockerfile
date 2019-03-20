FROM debian:sid-slim

ENV PACKAGES "curl openssh-client file git openssl ca-certificates wget golang-1.11-go jq unzip python3-minimal python3-requests python3-pip"

RUN apt-get update -y && \
  apt-get install -y $PACKAGES
RUN bash -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"

RUN pip3 install yq

RUN apt-get remove -y --purge python3-pip && \
    apt-get auto-remove -y && \
    rm -rf /var/lib/apt/lists/*
