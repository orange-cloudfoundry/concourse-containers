FROM orangeopensource/concourse:base-ruby

ENV CF_CLI_VERSION "6.28.0"
ARG BOSH_CLI_VERSION="1.3232.0"

ENV SPRUCE_VERSION "1.10.0"

ENV spiff_version "1.0.7"

ENV BOSH_CLI_GO_VERSION "2.0.27"

ENV BOSH_INIT_VERSION "0.0.103"

RUN gem install bosh_cli -v "$BOSH_CLI_VERSION"

ENV CREDHUB_CLI_VERSION "1.1.0"

RUN curl -L "https://cli.run.pivotal.io/stable?release=linux64-binary&version=${CF_CLI_VERSION}" | tar -zx -C /usr/local/bin

RUN curl -L "https://github.com/cloudfoundry-incubator/credhub-cli/releases/download/${CREDHUB_CLI_VERSION}/credhub-linux-${CREDHUB_CLI_VERSION}.tgz" | tar -zx -C /usr/local/bin

RUN curl -L "https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${BOSH_CLI_GO_VERSION}-linux-amd64" -o /usr/local/bin/bosh-cli \
&& chmod +x /usr/local/bin/bosh-cli

RUN curl -L "https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-${BOSH_INIT_VERSION}-linux-amd64" -o /usr/local/bin/bosh-init \
&& chmod +x /usr/local/bin/bosh-init

RUN apk add --update wget ca-certificates \
  && wget https://github.com/geofffranks/spruce/releases/download/v${SPRUCE_VERSION}/spruce-linux-amd64 \
  && chmod +x spruce-linux-amd64 \
  && mv spruce-linux-amd64 /usr/local/bin/spruce \
  && apk del wget ca-certificates \
  && rm -rf /var/cache/apk/*

RUN wget -O /tmp/spiff_linux_amd64.zip "https://github.com/cloudfoundry-incubator/spiff/releases/download/v${spiff_version}/spiff_linux_amd64.zip" && \
    unzip /tmp/spiff_linux_amd64.zip -d /usr/local/bin && \
    chmod 755 /usr/local/bin/spiff && \
    rm /tmp/spiff_linux_amd64.zip


