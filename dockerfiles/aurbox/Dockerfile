FROM docker.io/library/archlinux:base-devel

ENV NAME=archlinux-toolbox VERSION=base-devel
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Arch Linux toolbox containers"

RUN pacman -Syu --noconfirm git # upgrade everything and install git for AUR access


RUN git clone https://aur.archlinux.org/paru-bin.git && \ # paru for easy AUR access *optional
	chmod a+w /paru-bin && \ # *
	useradd -G wheel -m maker #*
COPY extra-packages /paru-bin/ #remap to '/' if not using paru
USER maker  # *
RUN cd paru-bin && \ #*
	makepkg -sicr --needed --noconfirm && \ #*
	paru -Syu --needed --noconfirm $(cat extra-packages | xargs) && \ # replace with `pacman` if not using paru
	paru -Scc --noconfirm # "   "
USER root

RUN rm -rf /paru-bin && \ #*
	userdel -rf maker && \ #*
	touch /etc/machine-id && \ # needed by toolbox
	mkdir -p /etc/sudoers.d && \
	echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox && \ # sudo access
	rm /etc/bash.bashrc # arch's bashrc has some compatibilty issues
	
CMD /bin/sh
