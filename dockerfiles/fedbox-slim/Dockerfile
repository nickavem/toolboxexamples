# Learn more about Fedora at: https://getfedora.org/
FROM registry.fedoraproject.org/fedora

ENV NAME=fedora-toolbox VERSION=34
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Install extra packages
RUN dnf -y install passwd

# Add the rpmfusion repo: https://rpmfusion.org/
RUN sudo dnf install -y \
	https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
	https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# These commands will help the image better integrate with the toolbox upstream:
# https://github.com/containers/toolbox#image-requirements
RUN touch /etc/host.conf /etc/hosts /etc/localtime /etc/resolv.conf /etc/timezone
RUN mkdir -p /etc/krb5.conf.d

# Also required to run, but not documented: https://github.com/containers/toolbox/pull/715
RUN touch /etc/machine-id

# This will give the group `wheel` sudo access on the host.
RUN mkdir -p /etc/sudoers.d
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox

# Cleanup
RUN dnf clean all

CMD /bin/sh
