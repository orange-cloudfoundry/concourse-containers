FROM ruby:2.3-slim-stretch

ENV PACKAGES "bash curl openssh-client file git openssl ca-certificates wget libffi-dev zip"


RUN apt-get update && apt-get install -y $PACKAGES && rm -rf /var/lib/apt/lists/*

RUN curl -L 'https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64' -o /usr/local/bin/jq && chmod +x /usr/local/bin/jq

RUN curl -L 'https://storage.googleapis.com/golang/go1.11.2.linux-amd64.tar.gz' -o go.tar.gz && tar -C /usr/local -xzf go.tar.gz && rm -f go.tar.gz

RUN mkdir -p /gopath/bin
ENV GOPATH /gopath
ENV GOBIN /gopath/bin
ENV PATH $PATH:/usr/local/go/bin:$GOPATH/bin
