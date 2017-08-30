FROM orangeopensource/concourse:base

ENV terraform_version "0.10.2"

ENV PROVIDER_CLOUDFOUNDRY_VERSION "v0.8.4"

ENV JSON2HCL_VERSION "v0.0.6"

RUN wget -O /tmp/terraform.zip "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip" && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/terraform && \
    rm /tmp/terraform.zip

RUN sh -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-provider-cloudfoundry/master/bin/install.sh)"

RUN curl -SsL https://github.com/kvz/json2hcl/releases/download/${JSON2HCL_VERSION}/json2hcl_${JSON2HCL_VERSION}_linux_amd64 \
	| tee /usr/local/bin/json2hcl > /dev/null && chmod +x /usr/local/bin/json2hcl