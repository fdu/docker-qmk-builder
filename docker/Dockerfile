FROM debian:buster

ENV USER deb
ENV UID 1000
ENV GID 1000
ENV DEBIAN_FRONTEND noninteractive

RUN apt update
RUN apt install -y python3-pip git avrdude dfu-programmer dfu-util gcc-arm-none-eabi gcc-avr
RUN useradd -rm -d /home/$USER -s /bin/bash -u $UID $USER
RUN pip3 install qmk

USER $USER
WORKDIR /home/$USER

RUN qmk clone
RUN qmk setup
