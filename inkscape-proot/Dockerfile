FROM alpine as rootfs

ARG DOCKER_ENDPOINT=taisun/random-images:inkscape-proot

# Install packages
RUN \
  echo "**** install packages ****" && \
  apk add --no-cache \
    bash \
    font-noto \
    inkscape \
    pulseaudio && \
  echo "**** customize desktop file ****" && \
  sed -i \
    "/Exec=/c Exec=/bin/sh -c \"\$HOME\/.local\/bin\/proot-apps run ${DOCKER_ENDPOINT}\"" \
    /usr/share/applications/org.inkscape.Inkscape.desktop && \
  echo "**** cleanup ****" && \
  rm -rf \
    /tmp/*

COPY ./entrypoint /entrypoint
COPY ./install /install
COPY ./remove /remove

FROM scratch
COPY --from=rootfs / /
