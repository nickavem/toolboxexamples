# Learn more about arch Linux here: https://archlinux.org/
# This image uses the AUR by default. Learn more here: https://aur.archlinux.org/
FROM docker.io/library/archlinux:base-devel

ENV NAME=archlinux-toolbox VERSION=base-devel
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      com.redhat.component="$NAME" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Fedora toolbox containers" \
      maintainer="Andrew Thurman <ajtbecool@gmail.com>"

# Tell pacman to install documentation
RUN sed -i '92,100d' /etc/pacman.conf

# Inititalize repos and upgrade.
# The other images are not uphraded by default, however due to pacman's nature it
# makes the most sense to do it here.
RUN pacman -Syu --noconfirm

# Install documentation not included in the default image
COPY missing-docs /
RUN pacman -Syu --noconfirm $(<missing-docs)
RUN rm /missing-docs

# Install the AUR helper paru: https://github.com/Morganamilo/paru
# If you do not wish to use the AUR modify as necesarry.
RUN pacman -Syu git --noconfirm
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

# Install extra-packages including some from the AUR to increase parity with upstream fedora image
COPY extra-packages /
RUN paru -Syu --noconfirm $(cat extra-packages | xargs)
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
