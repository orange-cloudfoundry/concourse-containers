FROM debian:sid-slim

ENV PACKAGES "curl openssh-client file git openssl ca-certificates wget golang-1.11-go jq unzip python3-minimal python3-requests"

RUN apt-get update -y && \
  apt-get install -y $PACKAGES

RUN bash -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    python3-pip \
    python3-setuptools \
 && pip3 --disable-pip-version-check --no-cache-dir install \
    yq \
 && apt-get remove -y --purge \
    python3-pip \
    python3-setuptools \
 && apt-get auto-remove -y \
 && rm -rf /var/lib/apt/lists/*
