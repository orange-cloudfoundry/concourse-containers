FROM orangeopensource/concourse:base-debian

ARG CF_CLI_VERSION="6.46.0"
ARG BOSH_CLI_VERSION="5.5.1"
ARG BBR_VERSION="1.5.1"
ARG CREDHUB_CLI_VERSION="2.5.2"


RUN curl -L "https://cli.run.pivotal.io/stable?release=linux64-binary&version=${CF_CLI_VERSION}" | tar -zx -C /usr/local/bin

RUN curl -L "https://github.com/cloudfoundry-incubator/credhub-cli/releases/download/${CREDHUB_CLI_VERSION}/credhub-linux-${CREDHUB_CLI_VERSION}.tgz" | tar -zx -C /usr/local/bin

RUN curl -L "https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${BOSH_CLI_VERSION}-linux-amd64" -o /usr/local/bin/bosh \
&& chmod +x /usr/local/bin/bosh && cp /usr/local/bin/bosh /usr/local/bin/bosh-cli


RUN curl -L https://github.com/cloudfoundry-incubator/bosh-backup-and-restore/releases/download/v${BBR_VERSION}/bbr-${BBR_VERSION}.tar | tar -x -C ./ \
  && mv releases/bbr /usr/local/bin/ && chmod +x /usr/local/bin/bbr && rm -Rf releases
