FROM docker.io/ubuntu:latest

ENV NAME=ubuntu-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers"

ENV DEBIAN_FRONTEND=noninteractive # skips interactive prompts like timezone and krb5 config
COPY extra-packages /
RUN apt-get update && \
	apt-get upgrade -y && \ 
	yes | unminimize && \ # "unminimizes" the image. brings back docs missing docs and a few other things
	apt-get -y install $(cat extra-packages | xargs) && \ # install extra packages
	rm /extra-packages && \ 
	apt-get clean

CMD /bin/sh
