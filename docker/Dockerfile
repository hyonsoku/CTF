FROM --platform=linux/amd64 ubuntu:23.04

RUN apt update && apt upgrade -y && apt install -y \
    # Web
    wget \
    curl \
    # File
    file \
    unzip \
    # Forensic
    exiftool \
    foremost \
    # Misc
    python3 \
    python3-pip
RUN useradd --create-home --shell /bin/bash hyonsoku

USER hyonsoku
WORKDIR /home/hyonsokuo