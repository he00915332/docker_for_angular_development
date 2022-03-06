FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

COPY ./init_base /var/project
RUN apt-get update && apt-get install -yq wget \
    git \
    vim \
    nano \
    sudo \
    cron \
    net-tools \
    iputils-ping \
    procps \
    systemd \
    supervisor \
    nodejs \
    libonig-dev \
    npm

# nvm node npm
ENV NVM_DIR /usr/local/.nvm
ENV NODE_VERSION stable

# Install nvm
RUN git clone https://github.com/creationix/nvm.git $NVM_DIR && \
    cd $NVM_DIR && \
    git checkout `git describe --abbrev=0 --tags`

# Install default version of Node.js
RUN source $NVM_DIR/nvm.sh && \
    nvm install $NODE_VERSION && \
    nvm install lts/boron && \
    nvm install lts/carbon && \
    nvm install lts/dubnium && \
    nvm install lts/erbium && \
    nvm alias default $NODE_VERSION && \
    nvm use default

# Add nvm.sh to .bashrc for startup...
RUN echo "source ${NVM_DIR}/nvm.sh" > $HOME/.bashrc && \
    source $HOME/.bashrc

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules

# timeZone
ENV TZ=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

RUN npm install -g @angular/cli
RUN npm i -g pm2

ENV HOST 0.0.0.0
WORKDIR /var/project/01WorkSpace/02Atimars

EXPOSE 5000
