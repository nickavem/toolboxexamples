# Learn more about Fedora at: https://getfedora.org/
FROM registry.fedoraproject.org/fedora:34

ENV NAME=fedora-toolbox VERSION=34
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Tell dnf to properly install documentation
RUN sed -i '/tsflags=nodocs/d' /etc/dnf/dnf.conf

# Install docs not included in the slim fedora image
COPY missing-docs /
RUN dnf -y reinstall $(<missing-docs)
RUN rm /missing-docs

# Install extra packages
COPY extra-packages /
RUN dnf -y install $(<extra-packages)
RUN rm /extra-packages

# Add the rpmfusion repo: https://rpmfusion.org/
RUN sudo dnf install -y https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Clean up
RUN dnf clean all

CMD /bin/sh
