FROM alpine:3

# variable "HELM_VERSION" and "PLUGIN_VERSION" must be passed as docker environment variables during the image build
# docker build --no-cache --build-arg HELM_VERSION=3.3.0 PLUGIN_VERSION=0.2.2 -t alpine/helm-unittest:3.3.0-0.2.2 .

ENV HELM_BASE_URL="https://get.helm.sh"
ENV HELM_TAR_FILE="helm-v3.3.0-linux-amd64.tar.gz"
ENV PLUGIN_URL="https://github.com/quintush/helm-unittest/"

RUN apk add --update --no-cache curl ca-certificates git bash && \
  curl -L ${HELM_BASE_URL}/${HELM_TAR_FILE} |tar xvz && \
  mv linux-amd64/helm /usr/bin/helm && \
  chmod +x /usr/bin/helm && \
  helm plugin install ${PLUGIN_URL} --version 0.2.2 && \
  rm -rf linux-amd64 && \
  apk del curl git bash && \
  rm -f /var/cache/apk/* ; 

WORKDIR /apps
VOLUME [ "/apps" ]

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT "/entrypoint.sh"
