# Learn more about alpine Linux here: https://alpinelinux.org/
# This is a "slim" image and may require the installation of extra packages
FROM docker.io/library/alpine:latest

ENV NAME=alpine-toolbox VERSION=latest
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Alpine toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Add extra packages for a working enviroment: https://github.com/containers/toolbox#image-requirements
RUN apk add shadow sudo bash libcap

# These commands will help the image better integrate with the toolbox upstream:
# https://github.com/containers/toolbox#image-requirements
RUN touch /etc/host.conf /etc/hosts /etc/localtime /etc/resolv.conf /etc/timezone
RUN mkdir /etc/krb5.conf.d

# This will give the group `wheel` sudo access on the host.
RUN mkdir -p /etc/sudoers.d
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox

# Also required to run, but not documented: https://github.com/containers/toolbox/pull/715
RUN touch /etc/machine-id

# glibc is needed to run the toolbox binary in alpine. this isn't optimal but a
# bug report exists: https://github.com/containers/toolbox/issues/772
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.33-r0/glibc-2.33-r0.apk
RUN apk add glibc-2.33-r0.apk

# Alpine's default /media directory confuses toolbox. This removal is nondestructive
# and should be remapped on container creation.
RUN rm -r /media

# Alpine does not contain /usr/lib/os-release by default. Not required, but will
# print a warning otherwise.
RUN ln -fs /etc/os-release /usr/lib/os-release

# Full `ncurses-terminfo` package is not needed, otherwise toolbox will print a warning.
RUN apk add ncurses-terminfo

CMD /bin/sh
