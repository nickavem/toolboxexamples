FROM ghcr.io/void-linux/void-linux:latest-thin-x86_64

ENV NAME=voidlinux-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Void toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Install extra packages
RUN xbps-install -Sy sudo shadow util-linux bash libcap-progs ncurses-base

# These commands will help the image better integrate with the toolbox upstream:
# https://github.com/containers/toolbox#image-requirements
RUN touch /etc/host.conf /etc/hosts /etc/localtime /etc/resolv.conf /etc/timezone
RUN mkdir -p /etc/krb5.conf.d

# Also required to run, but not documented: https://github.com/containers/toolbox/pull/715
RUN touch /etc/machine-id

# This will give the group `wheel` sudo access on the host.
RUN mkdir -p /etc/sudoers.d
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox

# Full `ncurses-base` package is  not needed, but otherwise toolbox will print a warning.
RUN xbps-install -Sy ncurses-base

# Void does not contain /usr/lib/os-release by default. Not required, but will
# print a warning otherwise.
RUN xbps-install -Sy runit-void
RUN ln -fs /etc/os-release /usr/lib/os-release

# Cleanup
RUN xbps-remove -O

CMD /bin/sh
