# Learn more about arch Linux here: https://archlinux.org/
# This image uses the AUR by default. Learn more here: https://aur.archlinux.org/
FROM docker.io/library/archlinux:base-devel

ENV NAME=archlinux-toolbox VERSION=base-devel
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Even though it isn't optimal archlinux just breaks without an upgrade
RUN pacman -Syu --noconfirm

# Install the AUR helper paru: https://github.com/Morganamilo/paru
# If you do not wish to use the AUR modify as necesarry.
RUN pacman -Sy git --noconfirm
RUN git clone https://aur.archlinux.org/paru-bin.git
RUN chmod a+w /paru-bin
# Paru can only be built as a regular user with sudo access
RUN useradd -G wheel -m maker
RUN mkdir -p /etc/sudoers.d
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox
USER maker
# This will build paru and install
RUN cd paru-bin && \
	makepkg -sicr --noconfirm

# Cleanup
RUN paru -Scc --noconfirm

# Switch back to root and clean up
USER root
RUN rm -rf /paru-bin
RUN userdel -rf maker

# These commands will help the image better integrate with the toolbox upstream:
# https://github.com/containers/toolbox#image-requirements
RUN touch /etc/host.conf /etc/hosts /etc/localtime /etc/resolv.conf /etc/timezone
RUN mkdir /etc/krb5.conf.d

# Also required to run, but not documented: https://github.com/containers/toolbox/pull/715
RUN touch /etc/machine-id

# Arch Linux's default bashrc has some issues with Fedora's: https://pagure.io/setup/pull-request/23
RUN rm /etc/bash.bashrc

CMD /bin/sh
