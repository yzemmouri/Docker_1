FROM debian

ENV TS3SERVER_LICENSE=accept

WORKDIR /home

EXPOSE 9987/udp 10011 30033

RUN apt-get update && apt-get upgrade -y && apt-get install -y wget bzip2 && \
	wget http://dl.4players.de/ts/releases/3.13.5/teamspeak3-server_linux_amd64-3.13.5.tar.bz2 && \
	tar xvf *.tar.bz2 && \
	rm *.tar.bz2

WORKDIR teamspeak3-server_linux_amd64

ENTRYPOINT sh ts3server_minimal_runscript.sh

#docker build -t ts3 .
#docker run -it --rm -p=9987:9987/udp  -p=10011:10011 -p=30033:30033 -e TS3SERVER_LICENSE=accept ts3