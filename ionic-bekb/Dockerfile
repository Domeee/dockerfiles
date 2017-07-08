FROM base/archlinux:latest

# enable multilib repo because we're going to use 32bit libs
RUN sed -i "/\[multilib\]/,/Include/"'s/^#//' /etc/pacman.conf
# system upgrade
RUN pacman -Syu base-devel expac yajl git nano --noconfirm --needed
RUN useradd -m -G wheel -s /bin/bash batman
RUN echo "batman:batman" | chpasswd
RUN echo 'batman  ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

USER batman
ENV PATH="/usr/bin/core_perl:${PATH}" EDITOR=nano
WORKDIR /home/batman
RUN mkdir cower && cd cower
RUN sudo curl -o PKGBUILD https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=cower
RUN makepkg PKGBUILD --skippgpcheck 
RUN sudo pacman -U cower-17-2-x86_64.pkg.tar.xz --noconfirm

WORKDIR /home/batman
RUN mkdir pacaur && cd pacaur
RUN sudo curl -o PKGBUILD https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=pacaur
RUN makepkg PKGBUILD --skippgpcheck 
RUN sudo pacman -U pacaur-4.7.10-1-any.pkg.tar.xz --noconfirm

RUN pacaur -S android-platform android-sdk-build-tools android-support android-support-repository --noconfirm --needed --noedit

#USER root
#ENV JAVA_HOME="/usr/bin/core_perl:${PATH}"

#curl -o PKGBUILD https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=cower
#makepkg PKGBUILD --skippgpcheck
# root
#pacman -U cower-17-2-x86_64.pkg.tar.xz

# batman
# add /usr/bin/core_perl to path
#curl -o PKGBUILD curl -o PKGBUILD https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=cower
#makepkg PKGBUILD --skippgpcheck
# root
#pacman -U cower-4.7.10-1-any.pkg.tar.xz

#cleanup

#batman
#pacaur -S android-platformAUR
#android-sdkAUR
#android-sdk-platform-toolsAUR
#android-sdk-build-toolsAUR



#RUN makepkg 