
FROM docker.io/alpine

ENV NAME=alpine-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers"

COPY extra-packages /
RUN apk update && \
	apk upgrade && \
	chmod +x extra-packages && \
	./extra-packages && \
        rm /extra-packages && \
	mkdir -p /etc/sudoers.d && \
	echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox && \
	wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
	wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-2.33-r0.apk && \
	apk add glibc-2.33-r0.apk && \
	touch /etc/machine-id && \
	rm -r /media && \
	cp /etc/os-release /usr/lib/os-release && \
	echo "alias fpaste='dpaste'" > /etc/bashrc
CMD /bin/sh
