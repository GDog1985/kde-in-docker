FROM msjpq/kde-vnc:bionic

ARG MONO_VER="4.9.4"
ARG GECKO_VER="2.47.1"

RUN mkdir /_install


# WINE Prereq
ADD https://dl.winehq.org/wine-builds/winehq.key /_install
RUN dpkg --add-architecture i386 && \
    add-apt-repository -y ppa:cybermax-dexter/sdl2-backport && \
    apt-key add /_install/winehq.key && \
    apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main' && \
    apt update


# WINE HQ
RUN apt install -y winehq-devel
RUN mkdir /usr/share/wine


# Mono
RUN mkdir /usr/share/wine/mono
ADD https://dl.winehq.org/wine/wine-mono/${MONO_VER}/wine-mono-${MONO_VER}.msi /usr/share/wine/mono


# Gecko
RUN mkdir /usr/share/wine/gecko
ADD https://dl.winehq.org/wine/wine-gecko/${GECKO_VER}/wine-gecko-${GECKO_VER}-x86.msi /usr/share/wine/gecko
ADD https://dl.winehq.org/wine/wine-gecko/${GECKO_VER}/wine-gecko-${GECKO_VER}-x86_64.msi /usr/share/wine/gecko


# Wine Tricks
ADD https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks /usr/bin
RUN chmod +x /usr/bin/winetricks


# Cleanup
RUN apt autoremove -y && \
    apt clean && \
    rm -r /_install
