# 
# Used for Docker Compose stuff.
# See https://github.com/cdrage/composefiles
#
# Must mount config.json to /etc/sensu/config.json !!
#
FROM ubuntu:latest

MAINTAINER Ilya Shevyrev <ilya.shevyrev@gmail.com>

ARG UBUNTU_FRONTEND=noninteractive
ARG DEBIAN_FRONTEND=noninteractive

#! System preparation
RUN apt-get update \
    && apt-get install -y sudo bash git supervisor joe mc netdiag curl python-pip openssh-server \
    && mkdir -p /var/log/supervisor /var/run/sshd /etc/supervisor/conf.d 

COPY supervisord.conf /etc/supervisor/supervisord.conf

COPY sshd.conf /etc/supervisor/conf.d/sshd.conf

#COPY postgres.conf /etc/supervisor/conf.d/postgres.conf

#RUN echo 'root:0Kernel!' | chpasswd

#RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN useradd -G sudo -d /home/ij -s /bin/bash ij \
    && mkdir -p /home/ij/.ssh \
    && chown -R ij:ij /home/ij \
    && chmod 700 /home/ij/.ssh/

RUN echo 'ij ALL=(ALL) NOPASSWD:ALL' | tee -a /etc/sudoers

ADD authorized_keys /home/ij/.ssh/authorized_keys

RUN chown ij:ij /home/ij/.ssh/authorized_keys \
    && chmod 600 /home/ij/.ssh/authorized_keys

#port
EXPOSE 5432
EXPOSE 5433
EXPOSE 22
#add
CMD ["/usr/bin/supervisord"]
