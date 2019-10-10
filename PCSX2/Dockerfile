FROM nvidia/opengl:1.1-glvnd-runtime

RUN apt-get update
RUN apt-get -y install software-properties-common
RUN add-apt-repository ppa:pcsx2-team/pcsx2-daily -y
RUN apt-get update
RUN apt-get -y install pcsx2-unstable

RUN chmod +x /usr/games/PCSX2-linux.sh
RUN chmod 0755 /usr/games/PCSX2

RUN adduser --disabled-password --gecos 'PCSX2 Client' pcsx2

WORKDIR /home/pcsx2

RUN ln -s /usr/games/PCSX2 /usr/local/bin/PCSX2

USER pcsx2

ENTRYPOINT ["PCSX2"]
CMD []
