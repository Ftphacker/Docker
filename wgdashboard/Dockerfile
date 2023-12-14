FROM ubuntu:20.04

LABEL user="Khramow Vladimir"
LABEL email="xramow.vova2016@yandex.ru"
LABEL desc="WireGuard"
LABEL version="1.1"

RUN apt-get update && apt-get upgrade -y &&\
	apt-get install -y python3 python3-pip git net-tools wireguard iproute2

RUN useradd -s /bin/bash user01 && \
	echo 'user01:user01' | chpasswd && \
	adduser user01 sudo && \
	echo "user01 ALL=(ALL:ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN git clone -b v3.0.6 https://github.com/donaldzou/WGDashboard.git wgdashboard

WORKDIR /wgdashboard/src

RUN chmod u+x ./wgd.sh

RUN ./wgd.sh install

RUN pip3 install -r ./requirements.txt

RUN chmod -R 755 /etc/wireguard

ENTRYPOINT ["./wgd.sh", "debug"]

EXPOSE 10086
EXPOSE 51820/udp
