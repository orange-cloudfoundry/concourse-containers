FROM orangeopensource/concourse:base

ARG CF_CLI_VERSION="6.47.2"
ARG AUTOPILOT_VERSION="0.0.8"
ARG ANTIFREEZE_VERSION="0.4.0"
ARG BG_RESTAGE_VERSION="1.1.0"

LABEL description="This image contains cf-${CF_CLI_VERSION} with \
autopilot-${AUTOPILOT_VERSION}, \
antifreeze-${ANTIFREEZE_VERSION}, \
and restage-${BG_RESTAGE_VERSION} \
plugins."

RUN curl -LSs "https://cli.run.pivotal.io/stable?release=linux64-binary&version=${CF_CLI_VERSION}" | \
    tar -zvx -C /usr/local/bin -- cf

RUN cf install-plugin -f \
  "https://github.com/contraband/autopilot/releases/download/${AUTOPILOT_VERSION}/autopilot-linux"

RUN cf install-plugin -f \
  "https://github.com/odlp/antifreeze/releases/download/v${ANTIFREEZE_VERSION}/antifreeze-linux"

RUN cf install-plugin -f \
  "https://github.com/orange-cloudfoundry/cf-plugin-bg-restage/releases/download/v${BG_RESTAGE_VERSION}/cf-plugin-bg-restage_linux_386"
