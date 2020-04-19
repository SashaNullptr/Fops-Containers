FROM alpine:latest

RUN apk add --update-cache \
    build-base \
    binutils \
    perl \
    xz-dev \
    mtools \
    cdrkit \
    syslinux-dev \
    git \
  && rm -rf /var/cache/apk/*

RUN git clone git://git.ipxe.org/ipxe.git /opt/ipxe

WORKDIR /opt/ipxe/src

RUN make -j$(nproc) bin/ipxe.usb
