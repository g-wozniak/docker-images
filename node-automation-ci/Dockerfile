FROM ubuntu:18.04

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN sed -i s/http/ftp/ /etc/apt/sources.list

RUN apt-get update --fix-missing

ENV DEBIAN_FRONTEND="noninteractive"

# So we can start normal work
RUN apt-get install -yq wget \
      alien

RUN apt-get install -yq libgconf-2-4 \
      gnupg2 \
      apt-transport-https \
      curl \
      ca-certificates \
      gnupg-agent \
      software-properties-common \
      imagemagick \
      ghostscript \
      poppler-utils

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

RUN add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"

# Install Docker
RUN apt-get update --fix-missing
RUN apt-get install -yq docker-ce docker-ce-cli containerd.io

# Pull NVM

# Install latest chrome dev package and fonts to support major charsets (Chinese, Japanese, Arabic, Hebrew, Thai and a few others)
# Note: this installs the necessary libs to make the bundled version of Chromium that Puppeteer
# installs, work.
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update \
    && apt-get install -y google-chrome-unstable fonts-ipafont-gothic fonts-wqy-zenhei fonts-thai-tlwg fonts-kacst \
      --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /src/*.deb

RUN chown -R root /usr/local
RUN mkdir /usr/local/nvm
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 12.19.0

RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.36.0/install.sh | bash

RUN source $NVM_DIR/nvm.sh \
    && nvm alias default $NODE_VERSION \
    && nvm use default

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules

ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN node -v

RUN npm -v

WORKDIR /app
