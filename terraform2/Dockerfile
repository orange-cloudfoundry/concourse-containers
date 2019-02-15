FROM orangeopensource/concourse:base-debian

ENV terraform_version "0.11.11"
ENV PROVIDER_CLOUDFOUNDRY_BRANCH "do-not-merge-ldap-user-handling"
ENV PROVIDER_CREDHUB_VERSION "0.12.1"
ENV PROVIDER_UAA_VERSION "0.9.0"
ENV JSON2HCL_VERSION "0.0.6"
#ENV TERRAFORM_RESTRICTOR_VERSION "v1.0.0"

# install terraform
RUN wget -O /tmp/terraform.zip "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip" && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/terraform && \
    rm /tmp/terraform.zip

# install terraform-provider-cloudfoundry
RUN mkdir -p /tmp/go
RUN export GOPATH=/tmp/go && \
  mkdir -p /tmp/go/src/github.com/terraform-providers/ && \
  cd /tmp/go/src/github.com/terraform-providers/ && \
  git clone -b ${PROVIDER_CLOUDFOUNDRY_BRANCH} https://github.com/mevansam/terraform-provider-cf.git terraform-provider-cloudfoundry  && \
  cd /tmp/go/src/github.com/terraform-providers/terraform-provider-cloudfoundry && \
  /usr/lib/go-1.11/bin/go build && \
  mkdir -p ~/.terraform.d/plugins/linux_amd64/ && \
  cp terraform-provider-cloudfoundry ~/.terraform.d/plugins/linux_amd64/terraform-provider-cloudfoundry

# install terraform-provider-credhub
ADD https://github.com/orange-cloudfoundry/terraform-provider-credhub/releases/download/v${PROVIDER_CREDHUB_VERSION}/terraform-provider-credhub_linux_amd64 ~/.terraform.d/plugins/linux_amd64/terraform-provider-credhub

# install terraform-provider-uaa
ADD https://github.com/orange-cloudfoundry/terraform-provider-uaa/releases/download/${PROVIDER_UAA_VERSION}/terraform-provider-uaa_linux_amd64             ~/.terraform.d/plugins/linux_amd64/terraform-provider-uaa

# install terraform-restrictor
RUN bash -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-restrictor/master/bin/install.sh)"

# install json2hcl
RUN curl -SsL https://github.com/kvz/json2hcl/releases/download/v${JSON2HCL_VERSION}/json2hcl_v${JSON2HCL_VERSION}_linux_amd64 \
	| tee /usr/local/bin/json2hcl > /dev/null && chmod +x /usr/local/bin/json2hcl
