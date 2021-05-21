FROM docker.io/library/archlinux:base-devel

ENV NAME=archlinux-toolbox VERSION=base-devel
LABEL com.github.containers.toolbox="true" \
      com.github.debarshiray.toolbox="true" \
      name="$NAME" \
      version="$VERSION" \
      usage="This image is meant to be used with the toolbox command" \
      summary="Base image for creating Arch Linux toolbox containers"

RUN pacman -Syu --noconfirm git 


RUN git clone https://aur.archlinux.org/paru-bin.git && \ 
	chmod a+w /paru-bin && \ 
	useradd -G wheel -m maker 
COPY extra-packages /paru-bin/ 
USER maker  
RUN cd paru-bin && \ 
	makepkg -sicr --needed --noconfirm && \ 
	paru -Syu --needed --noconfirm $(cat extra-packages | xargs) && \ 
	paru -Scc --noconfirm 
USER root

RUN rm -rf /paru-bin && \ 
	userdel -rf maker && \ 
	touch /etc/machine-id && \ 
	mkdir -p /etc/sudoers.d && \
	echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/10-toolbox && \
	rm /etc/bash.bashrc
	
CMD /bin/sh
