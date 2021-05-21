FROM docker.io/ubuntu:latest

ENV NAME=ubuntu-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers"

ENV DEBIAN_FRONTEND=noninteractive
COPY extra-packages /
RUN apt-get update && \
	apt-get upgrade -y && \ 
	yes | unminimize && \
	apt-get -y install $(cat extra-packages | xargs) && \
	rm /extra-packages && \ 
	apt-get clean

CMD /bin/sh
