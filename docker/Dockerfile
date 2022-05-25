FROM debian:bullseye
ENV DEBIAN_FRONTEND     noninteractive
ENV LANG                en_US.UTF-8
ENV LANGUAGE            en_US:en
ENV LC_ALL              en_US.UTF-8
#ENV USER                deb
#ENV UID                 1000
#ENV GID                 1000
RUN apt update
#RUN apt install -y --no-install-recommends sudo locales nano
#RUN sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen
#RUN locale-gen
#RUN echo '%sudo ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
#RUN groupadd --gid $GID $USER
#RUN useradd -rm -d /home/$USER -s /bin/bash -g $USER -G sudo -u $UID $USER
#WORKDIR                 /home/$USER
#RUN apt update
RUN apt install -y python3-pip git avrdude dfu-programmer dfu-util gcc-arm-none-eabi gcc-avr
RUN pip3 install qmk
#USER $USER
#WORKDIR /home/$USER
WORKDIR /root
RUN qmk clone
RUN qmk setup
