################## BASE IMAGE ######################
FROM ubuntu:latest

################## METADATA ######################
LABEL base_image="ubuntu:latest"
LABEL version="1"
LABEL software="diann"
LABEL software.version="2.0.0"
LABEL about.summary="DIA-NN - a universal software for data-independent acquisition (DIA) proteomics data processing."
LABEL about.home="https://github.com/vdemichev/DiaNN"
LABEL about.documentation="https://github.com/vdemichev/DiaNN"
LABEL about.license_file="https://github.com/vdemichev/DiaNN/releases/download/2.0/LICENSE.txt"
LABEL about.license="custom, see /usr/diann/2.0.0/LICENSE.txt"
LABEL about.tags="Proteomics"

################## MAINTAINER ######################
MAINTAINER Niko Pinter <niko.pinter@uniklinik-freiburg.de>

################## INSTALLATION ######################

ENV DEBIAN_FRONTEND noninteractive

## Update and install packages
RUN apt-get update -y && apt-get install -y \
    wget locales unzip \
 && sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen \
 && locale-gen

## Set working directory
WORKDIR /opt/software

## Download diann-1.9.1.Linux.zip and unzip
RUN wget https://github.com/vdemichev/DiaNN/releases/download/2.0/DIA-NN-2.0-Academia-Linux.zip && \
    unzip DIA-NN-2.0-Academia-Linux.zip && \
    rm DIA-NN-2.0-Academia-Linux.zip

RUN mkdir -p /usr/diann/2.0.0 && \
    mv /opt/software/diann-2.0/* /usr/diann/2.0.0 && \
    mv /usr/diann/2.0.0/diann-linux /usr/diann/2.0.0/diann

## Get LICENSE.txt
RUN wget https://github.com/vdemichev/DiaNN/releases/download/2.0/LICENSE.txt && \
    mv /opt/software/LICENSE.txt /usr/diann/2.0.0/LICENSE.txt

RUN chmod +x /usr/diann/2.0.0/diann

## Set environment variables
ENV PATH="/usr/diann/2.0.0:$PATH"
ENV LD_LIBRARY_PATH="/usr/diann/2.0.0:$LD_LIBRARY_PATH"

## Create symbolic links for libgomp-98b21ff3.so.1
RUN ln -s /usr/diann/2.0.0/libgomp-98b21ff3.so.1 /usr/diann/2.0.0/libgomp.so.1

WORKDIR /data/
