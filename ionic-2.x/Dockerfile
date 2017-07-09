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

RUN pacaur -S android-platform android-sdk-build-tools android-support android-support-repository nvm --noconfirm --needed --noedit

USER root
ENV JAVA_HOME="/usr/lib/jvm/java-7-openjdk" \
    ANDROID_HOME="/opt/android-sdk" \
    NODE_VERSION="4.4.7" \
    NVM_DIR="/usr/share/nvm" \
    NODE_PATH=$NVM_DIR/v$NODE_VERSION/lib/node_modules \
    PATH="${PATH}:/opt/android-sdk/platform-tools:/opt/android-sdk/tools:$NVM_DIR/v$NODE_VERSION/bin" \
    CODE="/code/app"
RUN . $NVM_DIR/init-nvm.sh \
    && nvm install $NODE_VERSION \
    && npm install -g cordova@6.1.1 ionic@2.2.3 grunt

# expose app, live reload
EXPOSE 8100 35729