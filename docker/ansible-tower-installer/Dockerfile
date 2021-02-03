FROM ubuntu:xenial

# Install common prereqs
RUN apt update && apt install -y \
    curl \
    tar

# Install ansible prereq
RUN apt install -y software-properties-common && \
    apt-add-repository --yes --update ppa:ansible/ansible && \
    apt install -y ansible

# Install kubectl prereq
RUN curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/v1.19.3/bin/linux/amd64/kubectl && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/  

# Install helm prereq
RUN curl -Lo helm.tar.gz https://get.helm.sh/helm-v3.5.1-linux-amd64.tar.gz && \
    tar -zxvf helm.tar.gz && \
    chmod +x linux-amd64/helm && \
    mv linux-amd64/helm /usr/local/bin/

# TODO: Install oc prereq

COPY . /ansible-tower-openshift-setup
WORKDIR /ansible-tower-openshift-setup

ENV INVENTORY_FILE="./inventory/local-docker-desktop"
ENV OPTIONS=""
ENV PLAYBOOK="install.yaml"

ARG REPO=""
ENV REPO=$REPO
ARG VERSION="latest"
ENV VERSION=$VERSION

ENTRYPOINT ansible-playbook -i "${INVENTORY_FILE}" -e image_repo=$REPO -e image_version=$VERSION -v $OPTIONS $PLAYBOOK