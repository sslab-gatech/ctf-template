FROM ubuntu:26.04

RUN useradd -m -s /bin/bash ctf

# enable 32-bit support + pwntool
RUN dpkg --add-architecture i386
RUN apt update
RUN apt install -y --no-install-recommends \
    libc6:i386 libstdc++6:i386 \
    build-essential gcc-multilib g++-multilib \
    python3 python3-pwntools \
    && rm -rf /var/lib/apt/lists/*
