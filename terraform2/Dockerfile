FROM orangeopensource/concourse:base-debian

ARG terraform_version="0.11.14"
ARG PROVIDER_CLOUDFOUNDRY_BRANCH="do-not-merge-ldap-user-handling"
ARG PROVIDER_CREDHUB_VERSION="0.12.1"
ARG PROVIDER_UAA_VERSION="0.9.0"
ARG JSON2HCL_VERSION="0.0.6"

# install terraform
RUN wget -qO /tmp/terraform.zip "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip" && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/terraform && \
    rm /tmp/terraform.zip

# install terraform-provider-cloudfoundry
RUN export GOPATH=/tmp/go \
 && mkdir -p "${BUILDPATH:=${GOPATH}/src/github.com/terraform-providers}" \
 && curl -fLSs "https://github.com/mevansam/terraform-provider-cf/archive/${PROVIDER_CLOUDFOUNDRY_BRANCH}.tar.gz" |\
    tar --transform 's#^[^/]*#terraform-provider-cloudfoundry#' -C "$BUILDPATH" -xz \
 && cd "${BUILDPATH}/terraform-provider-cloudfoundry" \
 && CGO_ENABLED=0 /usr/lib/go-1.11/bin/go build -a -ldflags "-s -w" -gcflags="all=-trimpath=$GOPATH" \
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

RUN apt-get update -y && \
  apt-get install -y yarnpkg && \
  rm -rf /var/lib/apt/lists/*

RUN yarnpkg global add terraform-plan-parser
