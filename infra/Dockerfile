FROM hashicorp/terraform

RUN apk --no-cache add \
 python3 \
 curl \
 which \
 bash \
 git \
 jq

RUN curl -sSL https://sdk.cloud.google.com | bash

ENV PATH $PATH:/root/google-cloud-sdk/bin
ENV CLOUDSDK_PYTHON=python3

RUN gcloud config set core/disable_usage_reporting true && \
  gcloud config set component_manager/disable_update_check true && \
  gcloud components install kubectl && \
  gsutil cp gs://terraform-validator/releases/2019-04-04/terraform-validator-linux-amd64 /tmp/ && \
  chmod 755 /tmp/terraform-validator-linux-amd64 && \
  mv /tmp/terraform-validator-linux-amd64 /usr/bin/terraform-validator && \
  terraform version
  
ENTRYPOINT ["/usr/bin/terraform-validator"]
