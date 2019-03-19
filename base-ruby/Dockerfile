FROM ruby:2.4-alpine

ARG JQ_VERSION="1.6"

RUN apk add --no-cache bash curl openssh-client file git openssl ca-certificates libc6-compat

COPY mktemp /usr/bin/mktemp

RUN curl -LSs "https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64" |\
    install /dev/stdin /usr/local/bin/jq

RUN sh -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"
