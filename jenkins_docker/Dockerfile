FROM jenkins:latest
MAINTAINER Raul <raul.mesa@claranet.es>

ENV DOCKER_VERSION 1.9.1
ENV COMPOSE_VERSION 1.5.2

USER root

RUN apt-get update && apt-get install -y git curl  && apt-get clean

RUN curl -fsSL https://test.docker.com/ | sh

# Install Docker binary
RUN wget -nv https://get.docker.com/builds/Linux/x86_64/docker-$DOCKER_VERSION -O /usr/bin/docker && \
  chmod +x /usr/bin/docker

# Install Docker Compose binary
RUN wget -nv https://github.com/docker/compose/releases/download/$COMPOSE_VERSION/docker-compose-Linux-x86_64 \
  -O /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

#RUN apt-get update && apt-get install -y docker.io
RUN usermod -aG docker jenkins


USER jenkins
