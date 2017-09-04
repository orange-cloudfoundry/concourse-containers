FROM orangeopensource/concourse:base-ruby

RUN apk add --update musl-dev gcc make g++ && rm -rf /var/cache/apk/*

RUN gem install cf-uaac -v 3.12.0 --no-rdoc --no-ri
