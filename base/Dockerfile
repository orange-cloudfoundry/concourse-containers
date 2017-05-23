FROM ruby:2.2-alpine

ENV PACKAGES "bash curl openssh-client file git openssl ca-certificates wget libc6-compat"

RUN apk add --update $PACKAGES && rm -rf /var/cache/apk/*

RUN mv /bin/mktemp $HOME/
COPY mktemp /bin/mktemp
RUN chmod +x /bin/mktemp


RUN curl -L 'https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64' -o /usr/local/bin/jq && chmod +x /usr/local/bin/jq

