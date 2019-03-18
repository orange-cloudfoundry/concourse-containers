FROM orangeopensource/concourse:base

ENV terraform_version "0.11.8"

ENV PROVIDER_CLOUDFOUNDRY_VERSION "v0.11.2"

ENV PROVIDER_CREDHUB_VERSION "v0.11.0"

ENV JSON2HCL_VERSION "v0.0.6"
ENV TERRAFORM_RESTRICTOR_VERSION "v1.0.0"

RUN curl -LSso /tmp/terraform.zip "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip" && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/terraform && \
    rm /tmp/terraform.zip

RUN sh -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-provider-cloudfoundry/master/bin/install.sh)"

RUN sh -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-provider-credhub/master/bin/install.sh)"

RUN sh -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-restrictor/master/bin/install.sh)"

RUN curl -SsL https://github.com/kvz/json2hcl/releases/download/${JSON2HCL_VERSION}/json2hcl_${JSON2HCL_VERSION}_linux_amd64 |\
    install -v /dev/stdin /usr/local/bin/json2hcl
