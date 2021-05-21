FROM registry.fedoraproject.org/fedora:34

ENV NAME=fedora-toolbox VERSION=34
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      com.redhat.component="$NAME" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers"

COPY missing-docs /
COPY extra-packages /

RUN sed -i '/tsflags=nodocs/d' /etc/dnf/dnf.conf && \ 
	dnf upgrade -y && \
	dnf -y reinstall $(<missing-docs) && \ 
	rm /missing-docs && \ 
	dnf -y install $(<extra-packages) && \ 
	rm /extra-packages && \ 
	dnf install -y https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm && \
	dnf clean all

CMD /bin/sh
