FROM orangeopensource/concourse:base

ENV terraform_version "0.9.5"

ENV PROVIDER_CLOUDFOUNDRY_VERSION "v0.7.3"

RUN wget -O /tmp/terraform.zip "https://releases.hashicorp.com/terraform/${terraform_version}/terraform_${terraform_version}_linux_amd64.zip" && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    chmod +x /usr/local/bin/terraform && \
    rm /tmp/terraform.zip

RUN sh -c "$(curl -fsSL https://raw.github.com/orange-cloudfoundry/terraform-provider-cloudfoundry/master/bin/install.sh)"
