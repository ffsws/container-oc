FROM docker.io/library/centos:7@sha256:285bc3161133ec01d8ca8680cd746eecbfdbc1faa6313bd863151c4b26d7e5a5

ENV VERSION=v3.7.2 \
    HELM_VERSION=v2.16.1 \
    KUSTOMIZE_VERSION=v3.5.4 \
    IMAGE_CLEANUP_VERSION=v0.2.0 \
    KUBEVAL_VERSION=0.14.0 \
    ARCHIVE=openshift-origin-client-tools-v3.7.2-282e43f-linux-64bit \
    SHA256SUM=abc89f025524eb205e433622e59843b09d2304cc913534c4ed8af627da238624 \
    HELM_SHA256SUM=7eebaaa2da4734242bbcdced62cc32ba8c7164a18792c8acdf16c77abffce202 \
    KUSTOMIZE_SHA256SUM=5cdeb2af81090ad428e3a94b39779b3e477e2bc946be1fe28714d1ca28502f6a \
    IMAGE_CLEANUP_SHA256SUM=d9980626276d9f4acaf1a5f47d618e5bfacd97c5aa08e3e3f59fabbe8ac92712 \
    KUBEVAL_SHA256SUM=8b1b8c63df9ee3206113a3352e07474ea071610cfacf40a64db74c56e163f1e2 \
    SOPS_VERSION=v3.5.0 \
    SOPS_RELEASES_URL="https://github.com/mozilla/sops/releases/download" \
    OKD_RELEASES_URL="https://github.com/openshift/origin/releases/download" \
    HELM_RELEASES_URL="https://storage.googleapis.com/kubernetes-helm" \
    KUSTOMIZE_RELEASES_URL="https://github.com/kubernetes-sigs/kustomize/releases/download" \
    IMAGE_CLEANUP_RELEASES_URL="https://github.com/appuio/image-cleanup/releases/download" \
    KUBEVAL_RELEASES_URL="https://github.com/instrumenta/kubeval/releases/download" \
    JQ_URL="https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64" \
    OC_PLUGINS_REPO="https://github.com/appuio/oc-plugins" \
    KUBECTL_PLUGINS_PATH="/opt/kube/plugins"

RUN set -x && \
    URL="${OKD_RELEASES_URL}/${VERSION}/${ARCHIVE}.tar.gz" && \
    HELM_URL="${HELM_RELEASES_URL}/helm-${HELM_VERSION}-linux-amd64.tar.gz" && \
    KUSTOMIZE_URL="${KUSTOMIZE_RELEASES_URL}/kustomize%2F${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_amd64.tar.gz" && \
    IMAGE_CLEANUP_URL="${IMAGE_CLEANUP_RELEASES_URL}/${IMAGE_CLEANUP_VERSION}/image-cleanup_linux_amd64" && \
    KUBEVAL_URL="${KUBEVAL_RELEASES_URL}/${KUBEVAL_VERSION}/kubeval-linux-amd64.tar.gz" && \
    SOPS_URL="${SOPS_RELEASES_URL}/${SOPS_VERSION}/sops-${SOPS_VERSION}.linux" && \
    cd /tmp && \
    curl -sSL "$URL" -o /tmp/oc.tgz && \
    curl -sSL "$HELM_URL" -o /tmp/helm.tgz && \
    curl -sSL "$KUSTOMIZE_URL" -o /tmp/kustomize.tgz && \
    curl -sSL "$IMAGE_CLEANUP_URL" -o /tmp/image-cleanup && \
    curl -sSL "$KUBEVAL_URL" -o /tmp/kubeval.tgz && \
    curl -sSL "$JQ_URL" -o /tmp/jq && \
    curl -sSL "$SOPS_URL" -o /bin/sops && \
    echo "${SHA256SUM}  /tmp/oc.tgz" > /tmp/CHECKSUM && \
    echo "${HELM_SHA256SUM}  /tmp/helm.tgz" > /tmp/HELM_CHECKSUM && \
    echo "${KUSTOMIZE_SHA256SUM}  /tmp/kustomize.tgz" > /tmp/KUSTOMIZE_CHECKSUM && \
    echo "${IMAGE_CLEANUP_SHA256SUM}  /tmp/image-cleanup" > /tmp/IMAGE_CLEANUP_CHECKSUM && \
    echo "${KUBEVAL_SHA256SUM}  /tmp/kubeval.tgz" > /tmp/KUBEVAL_CHECKSUM && \
    sha256sum -c /tmp/CHECKSUM && \
    sha256sum -c /tmp/HELM_CHECKSUM && \
    sha256sum -c /tmp/KUSTOMIZE_CHECKSUM && \
    sha256sum -c /tmp/IMAGE_CLEANUP_CHECKSUM && \
    sha256sum -c /tmp/KUBEVAL_CHECKSUM && \
    tar -xzvf /tmp/oc.tgz && \
    tar -xzvf /tmp/helm.tgz && \
    tar -xzvf /tmp/kustomize.tgz && \
    tar -xzvf /tmp/kubeval.tgz && \
    chmod 755 /tmp/kustomize /tmp/image-cleanup /tmp/jq /bin/sops && \
    mv -v "/tmp/${ARCHIVE}/oc" /bin/ && \
    mv -v "/tmp/linux-amd64/helm" /bin/ && \
    mv -v "/tmp/kubeval" /bin/ && \
    mv -v "/tmp/kustomize" /bin/ && \
    mv -v "/tmp/image-cleanup" /bin/ && \
    mv -v "/tmp/jq" /bin/ && \
    ln -s /bin/oc /bin/kubectl && \
    rm -rf /tmp/* && \
    yum install -y git gettext && \
    yum clean all -y && \
    git clone --depth=1 ${OC_PLUGINS_REPO} ${KUBECTL_PLUGINS_PATH}
