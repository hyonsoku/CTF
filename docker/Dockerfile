FROM --platform=linux/amd64 ubuntu:23.04

RUN apt update && apt upgrade -y && apt install -y \
    wget \
    curl \
    file
RUN useradd --create-home --shell /bin/bash hyonsoku

USER hyonsoku
WORKDIR /home/hyonsoku