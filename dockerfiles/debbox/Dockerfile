# Learn more about Debian at: https://www.debian.org/
FROM docker.io/library/debian

ENV NAME=debian-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      com.redhat.component="$NAME" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Debian toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Updates package database but not packages
RUN apt-get update

# Install extra packages
COPY extra-packages /
RUN apt-get -y install $(cat extra-packages | xargs)
RUN rm /extra-packages

# Cleanup
RUN apt-get clean

# This will give the group `wheel` sudo access on the host.
# For some reason sudo is slow on debian. If anyone can figure out why please let
# me know.
RUN mkdir -p /etc/sudoers.d
RUN sed -i "s/nullok_secure/nullok/" /etc/pam.d/common-auth
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox
RUN apt-get install libnss-myhostname

CMD /bin/sh
