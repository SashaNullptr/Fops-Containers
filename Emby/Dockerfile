FROM nvidia/opengl:1.1-glvnd-runtime

RUN dpkg-reconfigure debconf -f noninteractive -p critical

RUN apt-get update && \
apt-get -y install wget

RUN wget \
https://github.com/MediaBrowser/Emby.Releases/releases/download/4.2.1.0/emby-server-deb_4.2.1.0_amd64.deb && \
dpkg -i emby-server-deb_4.2.1.0_amd64.deb && \
rm emby-server-deb_4.2.1.0_amd64.deb
