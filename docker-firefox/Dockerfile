FROM ghcr.io/linuxserver/baseimage-rdesktop-web:3.16

# set version label
ARG BUILD_DATE
ARG VERSION
ARG FIREFOX_VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="Zmey Goryth"

RUN \
  echo "**** install packages ****" && \
  if [ -z ${FIREFOX_VERSION+x} ]; then \
    FIREFOX_VERSION=$(curl -sL "http://dl-cdn.alpinelinux.org/alpine/v3.16/community/x86_64/APKINDEX.tar.gz" | tar -xz -C /tmp \
    && awk '/^P:firefox$/,/V:/' /tmp/APKINDEX | sed -n 2p | sed 's/^V://'); \
  fi && \
  apk add --no-cache \
    firefox==${FIREFOX_VERSION} && \
  sed -i 's|</applications>|  <application title="Mozilla Firefox" type="normal">\n    <maximized>yes</maximized>\n  </application>\n</applications>|' /etc/xdg/openbox/rc.xml && \
  echo "**** cleanup ****" && \
  rm -rf \
    /tmp/*

RUN apk add scrot

RUN apk add vim

RUN apk update

RUN apk add ffmpeg

RUN apk add pulseaudio pulseaudio-alsa

RUN apk add alsa-plugins-pulse
# add local files
COPY /root /

# ports and volumes
EXPOSE 3000

RUN chmod +777 /config

VOLUME /config


