# Learn more about Debian at: https://www.debian.org/
FROM docker.io/library/debian:stable-slim

ENV NAME=debian-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Debian toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Updates package database but not packages
RUN apt-get update

# Add extra packages
RUN apt-get install -y libnss-myhostname sudo libcap2-bin

# This will give the group `wheel` sudo access on the host.
# For some reason sudo is slow on debian. If anyone can figure out why please let
# me know.
RUN mkdir -p /etc/sudoers.d
RUN sed -i "s/nullok_secure/nullok/" /etc/pam.d/common-auth
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox

# These commands will help the image better integrate with the toolbox upstream:
# https://github.com/containers/toolbox#image-requirements
RUN touch /etc/host.conf /etc/hosts /etc/localtime /etc/resolv.conf /etc/timezone
RUN mkdir /etc/krb5.conf.d

# Also required to run, but not documented: https://github.com/containers/toolbox/pull/715
RUN touch /etc/machine-id

# Clean up
RUN apt-get autoclean && apt-get clean

CMD /bin/sh
