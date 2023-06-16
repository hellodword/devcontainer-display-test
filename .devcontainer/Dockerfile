ARG VARIANT="jammy"
FROM buildpack-deps:${VARIANT}-curl

LABEL dev.containers.features="common"

RUN apt-get update

RUN env DEBIAN_FRONTEND=noninteractive apt-get install --yes \
    ca-certificates \
    bash-completion \
    curl \
    git \
    vim \
    locales ttf-wqy-zenhei sudo tzdata \
    libxext6 libxrender1 libxtst6 libxi6 \
    libglib2.0-0 libx11-xcb1 \
    # libqt5gui5 \
    # libgtk-3-0 \
    # libcanberra-gtk3-module \
    software-properties-common \
    --no-install-recommends

ENV EDITOR=vim

# configure locales to UTF8
RUN apt-get install locales && locale-gen en_US.UTF-8
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN add-apt-repository ppa:saiarcot895/chromium-beta && \
    env DEBIAN_FRONTEND=noninteractive apt-get install -y chromium-browser

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME

RUN echo "$USERNAME ALL=(ALL) NOPASSWD:ALL">/etc/sudoers.d/90-cloud-init-users

# need --no-sandbox for chromium
