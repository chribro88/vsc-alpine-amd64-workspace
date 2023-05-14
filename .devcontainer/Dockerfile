#-------------------------------------------------------------------------------------------------------------
# mostly adapted from https://github.com/senglin and https://github.com/Docker-Hub-frolvlad
#-------------------------------------------------------------------------------------------------------------
ARG REGISTRY_HOST=
ARG REGISTRY_USERNAME=

ARG BASE_VERSION=3.18

FROM ${REGISTRY_HOST}/${REGISTRY_USERNAME}/alpine-miniconda3:${BASE_VERSION}

ARG USERNAME=vsc
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG DOCKER_GID=998

ENV HOME /home/$USER

RUN apk --update --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing --repository http://dl-cdn.alpinelinux.org/alpine/edge/main add \
                curl \
                # git, process tools, lsb-release (common in install instructions for CLIs) installed
                git openssh-client zip vim less iproute2 procps lsb-release upx file make \
                # build-essential \
                build-base gcc \
                # vscode
                libstdc++6 \
                # bash - helps for conda init
                bash \
                # build third party python libraries
                python3-dev \
                # SSL dependencies
                #apt-transport-https ca-certificates gnupg2
                ca-certificates gnupg \
                # https://wiki.alpinelinux.org/wiki/Docker
                openrc \
                # other useful tools
                nano \
                # non-root docker
                shadow-uidmap \
                # https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user
                shadow
                # # sudo
                # sudo 
                
RUN \
    # create vscode user and group
    # https://github.com/mhart/alpine-node/issues/48#issuecomment-370171836
    addgroup -g $USER_GID -S $USERNAME \
    && adduser -u $USER_UID -S $USERNAME -G $USERNAME -s /bin/bash \
    # create docker group
    && addgroup -g $DOCKER_GID docker \
    # add user to docker group
    && usermod -a -G docker $USERNAME

# # Docker installation
RUN \
    apk --update --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing --repository http://dl-cdn.alpinelinux.org/alpine/edge/main add \
    docker docker-compose \
    && rc-update add cgroups \
    && rc-update add docker default \
    && echo $USERNAME:100000:65536 >/etc/subuid \
    && echo $USERNAME:100000:65536 >/etc/subuid

# copy over the conda environment setup script
COPY --chown=1000 .devcontainer/postCreateCommand.sh \
     .devcontainer/environment.yml* /tmp/conda-tmp/

RUN chmod +x /tmp/conda-tmp/postCreateCommand.sh

# make user sudoer
# RUN echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$USERNAME \
#     && chmod 0440 /etc/sudoers.d/$USERNAME

# Clean up
RUN rm -rf /var/cache/apk/*

# Forward ports
EXPOSE 5000
