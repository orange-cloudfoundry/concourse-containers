FROM debian:stretch-slim

ENV PACKAGES "curl openssh-client file git openssl ca-certificates wget golang-1.11-go jq unzip python3-minimal python3-requests"

RUN apt-get update -y && \
  apt-get install -y $PACKAGES

RUN bash -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"
RUN curl -fL https://getcli.jfrog.io | sh && mv jfrog /usr/local/bin/
RUN curl -fL https://github.com/cloudfoundry/bosh-cli/releases/download/v5.4.0/bosh-cli-5.4.0-linux-amd64 | install /dev/stdin /usr/local/bin/bosh

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
