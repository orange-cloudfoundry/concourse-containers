FROM orangeopensource/concourse:base-debian

ARG terraform_version="0.11.14"
ARG PROVIDER_CLOUDFOUNDRY_BRANCH="rework-back"
ARG PROVIDER_CREDHUB_VERSION="0.12.1"
ARG PROVIDER_UAA_VERSION="0.9.0"
ARG JSON2HCL_VERSION="0.0.6"
ARG PROVIDER_CFSECURITY_VERSION="0.1.6"
ARG PROVIDER_CLOUDFOUNDRY_LEGACY_TERRAFORM="1"
ARG TERRAFORM_RESTRICTOR_VERSION="v1.0.0"

# install terraform
RUN wget -qO /tmp/terraform.zip "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip" && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/terraform && \
    rm /tmp/terraform.zip

# install terraform-provider-cloudfoundry
RUN export GOPATH=/tmp/go \
 && mkdir -p "${BUILDPATH:=/tmp}" \
 && curl -fLSs "https://github.com/mevansam/terraform-provider-cf/archive/${PROVIDER_CLOUDFOUNDRY_BRANCH}.tar.gz" |\
    tar xz -C "${BUILDPATH}" \
 && cd "${BUILDPATH}/terraform-provider-cf-${PROVIDER_CLOUDFOUNDRY_BRANCH}" \
 && if test "${PROVIDER_CLOUDFOUNDRY_LEGACY_TERRAFORM}" -eq 1; then sed -i 's%github.com/hashicorp/terraform v0.12.0%github.com/hashicorp/terraform v0.11.14%g' go.mod; fi  \
 && go mod download \
 && CGO_ENABLED=0 /usr/local/go/bin/go build -a -ldflags="-s -w" \
 && install -D terraform-provider-cloudfoundry ~/.terraform.d/plugins/linux_amd64/terraform-provider-cloudfoundry \
 && rm -fr "$GOPATH" "${HOME}/.cache/go-build"

# install terraform-provider-credhub
RUN curl -fLSs "https://github.com/orange-cloudfoundry/terraform-provider-credhub/releases/download/v${PROVIDER_CREDHUB_VERSION}/terraform-provider-credhub_linux_amd64" |\
    install -D -s /dev/stdin ~/.terraform.d/plugins/linux_amd64/terraform-provider-credhub

# install terraform-provider-uaa
RUN curl -fLSs "https://github.com/orange-cloudfoundry/terraform-provider-uaa/releases/download/${PROVIDER_UAA_VERSION}/terraform-provider-uaa_linux_amd64" |\
    install -D -s /dev/stdin ~/.terraform.d/plugins/linux_amd64/terraform-provider-uaa

# install terraform-restrictor
RUN bash -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-restrictor/master/bin/install.sh)"

# install json2hcl
RUN curl -fSsL "https://github.com/kvz/json2hcl/releases/download/v${JSON2HCL_VERSION}/json2hcl_v${JSON2HCL_VERSION}_linux_amd64" |\
    install -D -s /dev/stdin /usr/local/bin/json2hcl

# install terraform-provider-cfsecurity
RUN true \
 && mkdir -p "${BUILDPATH:=/tmp/}" \
 && curl -fLSs "https://github.com/orange-cloudfoundry/cf-security-entitlement/archive/v${PROVIDER_CFSECURITY_VERSION}.tar.gz" | \
    tar xz -C "${BUILDPATH}" \
 && cd "${BUILDPATH}/cf-security-entitlement-${PROVIDER_CFSECURITY_VERSION}/" \
 && if test "${PROVIDER_CLOUDFOUNDRY_LEGACY_TERRAFORM}" -eq 1; then sed -i 's%github.com/hashicorp/terraform v0.12.0%github.com/hashicorp/terraform v0.11.14%g' go.mod; fi  \
 && go mod download \
 && cd terraform-provider-cfsecurity \
 && /usr/local/go/bin/go build -ldflags="-s -w" \
 && install -D terraform-provider-cfsecurity ~/.terraform.d/plugins/linux_amd64/terraform-provider-cfsecurity \
 && rm -fr "${HOME}/.cache/go-build" ${BUILDPATH}/cf-security-entitlement-${PROVIDER_CFSECURITY_VERSION}


# install yarn, nodejs and terraform-plan-parser
RUN apt-get update -y && \
  apt-get install -y gnupg  && \
  rm -rf /var/lib/apt/lists/*
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
 && apt-get install -y nodejs
RUN wget https://github.com/yarnpkg/yarn/releases/download/v1.17.3/yarn_1.17.3_all.deb && dpkg -i yarn_1.17.3_all.deb
RUN yarnpkg --version
RUN yarnpkg global add terraform-plan-parser
RUN go clean -modcache