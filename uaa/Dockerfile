FROM orangeopensource/concourse:base-ruby

ARG CF_UAAC_VERSION=3.12.0

RUN apk add --no-cache musl-dev gcc make g++

RUN gem install cf-uaac -v "${CF_UAAC_VERSION}"

FROM orangeopensource/concourse:base-ruby

RUN apk add --no-cache libstdc++

COPY --from=0 /usr/local/bundle /usr/local/bundle
