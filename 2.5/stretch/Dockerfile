FROM circleci/ruby:2.5-stretch

# OS packages
RUN echo 'APT::Install-Recommends "false";' | sudo tee /etc/apt/apt.conf.d/no-install-recommends >/dev/null && \
  sudo apt-get update && \
  sudo apt-get install -y \
    apt-transport-https \
    protobuf-compiler mysql-client python3-pip python3-setuptools python3-yaml python3-wheel python3-dev && \
  sudo rm -rf /var/lib/apt/lists/*

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - && \
  sudo apt-get install nodejs && \
  sudo npm install -g yarn && \
  sudo rm -rf /var/lib/apt/lists/* && \
  sudo rm -rf /tmp/npm-*

# AWS CLI
RUN sudo pip3 install awscli && \
  sudo rm -rf /tmp/pip*

# ChromeDriver
ENV CHROMEDRIVER_PATH /usr/local/bin/chromedriver
RUN sudo apt-get update && \
  sudo apt-get install -y chromium libgconf-2-4 unzip && \
  sudo rm -rf /var/lib/apt/lists/*
RUN VERSION=$(curl -sL https://chromedriver.storage.googleapis.com/LATEST_RELEASE) && \
  curl -L -o /tmp/chromedriver.zip https://chromedriver.storage.googleapis.com/${VERSION}/chromedriver_linux64.zip && \
  unzip -d /tmp /tmp/chromedriver.zip && \
  sudo cp /tmp/chromedriver /usr/local/bin/chromedriver && \
  rm -f /tmp/chromedriver*
