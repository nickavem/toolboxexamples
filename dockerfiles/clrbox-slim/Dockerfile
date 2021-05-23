# Learn more about Clear Linux at: https://clearlinux.org/
# ***THIS IMAGE USES SOME SKETCHY WORKAROUNDS. USE AT YOUR OWN RISK***
FROM docker.io/library/clearlinux:latest

ENV NAME=clearlinux-toolbox VERSION=34
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Clear Linux toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Install extra packages
RUN swupd bundle-add sudo

# These commands will help the image better integrate with the toolbox upstream:
# https://github.com/containers/toolbox#image-requirements
RUN touch /etc/host.conf /etc/hosts /etc/localtime /etc/resolv.conf /etc/timezone
RUN mkdir -p /etc/krb5.conf.d

# Also required to run, but not documented: https://github.com/containers/toolbox/pull/715
RUN touch /etc/machine-id

# This will give the group `wheel` sudo access on the host.
RUN mkdir -p /etc/sudoers.d
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox

# ***Configure toolbox to work with clear's weird filesystem heirarchy
RUN ln /usr/share/defaults/etc/passwd /etc/passwd
RUN ln /usr/share/defaults/etc/group /etc/group

# Clean
RUN swupd clean
