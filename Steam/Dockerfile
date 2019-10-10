FROM nvidia/opengl:1.0-glvnd-runtime

RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y wget gdebi-core libgl1-mesa-dri:i386 libgl1-mesa-glx:i386
RUN wget http://media.steampowered.com/client/installer/steam.deb
RUN gdebi -n ./steam.deb

RUN adduser --disabled-password --no-create-home --gecos 'Steam Client' --home /opt/steam steam
RUN mkdir -p /opt/steam /var/lib/steam /home/steam/.steam/steam/steamapps/common
RUN chown -R steam:steam /opt/steam /var/lib/steam /home/steam/.steam/steam/steamapps/common

# Preseed dpkg to skip license agreement
RUN echo steam steam/license note '' | debconf-set-selections
RUN echo steam steam/question select "I AGREE" | debconf-set-selections

# Install steam command line tools
RUN apt-get install -y steamcmd
RUN ln -s /usr/games/steamcmd /usr/local/bin/steamcmd

USER steam
WORKDIR /var/lib/steam

# Bootstraps the Steam client
RUN steamcmd +login anonymous validate +quit

# Updates on launch
ONBUILD RUN steamcmd +login anonymous validate +quit

ENTRYPOINT ["steam"]
CMD []
