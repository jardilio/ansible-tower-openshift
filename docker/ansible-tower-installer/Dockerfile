# Allow user to base this from centos or rhel
ARG BASE="centos:7"
# ARG BASE="registry.redhat.io/rhel7/rhel"

FROM ${BASE}

# Install ansible prereq
RUN yum install -y epel-release-7-11 && \
    yum install -y ansible-2.9.16-1.el7

# Install oc and kubctl prereq
RUN curl -Lo openshift-client-linux.tar.gz https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/openshift-client-linux-4.6.16.tar.gz && \
    tar -zxvf openshift-client-linux.tar.gz && \
    chmod +x oc && \
    mv oc /usr/local/bin/ && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/

# Install helm prereq (only required if running postgres in-cluster)
RUN curl -Lo helm.tar.gz https://get.helm.sh/helm-v3.5.1-linux-amd64.tar.gz && \
    tar -zxvf helm.tar.gz && \
    chmod +x linux-amd64/helm && \
    mv linux-amd64/helm /usr/local/bin/

# Install git prereq
RUN yum install -y git

# Copy our playbook and supporting files into the image as part of release
COPY . /ansible-tower-openshift-setup
WORKDIR /ansible-tower-openshift-setup

# Set default options for entrypoint that user can override
ENV INVENTORY_FILE="./inventory/local-docker-desktop"
ENV OPTIONS=""
ENV PLAYBOOK="install.yaml"

ARG REPO=""
ENV REPO=$REPO
ARG VERSION="latest"
ENV VERSION=$VERSION

ENTRYPOINT ansible-playbook -i "${INVENTORY_FILE}" -e image_repo=$REPO -e image_version=$VERSION -v $OPTIONS $PLAYBOOK