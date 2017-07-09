FROM orangeopensource/concourse:base

ENV CF_CLI_VERSION "6.28.0"

ENV AUTOPILOT_VERSION "0.0.3"

ENV AUTOPILOT_TEMPFILE "/tmp/autopilot-linux"

ENV ANTIFREEZE_VERSION "0.3.0"

ENV ANTIFREEZE_TEMPFILE "/tmp/antifreeze-linux"

ENV BG_RESTAGE_VERSION "1.0.0"

ENV BG_RESTAGE_TEMPFILE "/tmp/bg-restage-linux"

RUN apk add --update musl-dev gcc make g++ && rm -rf /var/cache/apk/*

RUN gem install cf-uaac -v 3.12.0 --no-rdoc --no-ri

RUN curl -L "https://cli.run.pivotal.io/stable?release=linux64-binary&version=${CF_CLI_VERSION}" | tar -zx -C /usr/local/bin

RUN curl -L -o "${AUTOPILOT_TEMPFILE}" \
  "https://github.com/contraband/autopilot/releases/download/${AUTOPILOT_VERSION}/autopilot-linux" \
  && chmod +x "${AUTOPILOT_TEMPFILE}" \
  && cf install-plugin -f "${AUTOPILOT_TEMPFILE}" \
  && rm "${AUTOPILOT_TEMPFILE}"

RUN curl -L -o "${ANTIFREEZE_TEMPFILE}" \
  "https://github.com/odlp/antifreeze/releases/download/v${ANTIFREEZE_VERSION}/antifreeze-linux" \
  && chmod +x "${ANTIFREEZE_TEMPFILE}" \
  && cf install-plugin -f "${ANTIFREEZE_TEMPFILE}" \
  && rm "${ANTIFREEZE_TEMPFILE}"

RUN curl -L -o "${BG_RESTAGE_TEMPFILE}" \
  "https://github.com/orange-cloudfoundry/cf-plugin-bg-restage/releases/download/v${BG_RESTAGE_VERSION}/cf-plugin-bg-restage_linux_amd64" \
  && chmod +x "${BG_RESTAGE_TEMPFILE}" \
  && cf install-plugin -f "${BG_RESTAGE_TEMPFILE}" \
  && rm "${BG_RESTAGE_TEMPFILE}"
