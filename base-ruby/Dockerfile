FROM ruby:2.4-alpine


RUN apk add --no-cache bash curl openssh-client file git openssl ca-certificates libc6-compat

COPY mktemp /usr/bin/mktemp


RUN curl -L 'https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64' -o /usr/local/bin/jq && chmod +x /usr/local/bin/jq

RUN sh -c "$(curl -fsSL https://raw.github.com/ArthurHlt/notifslack/master/bin/install.sh)"
