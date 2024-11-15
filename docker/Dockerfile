FROM ubuntu:22.04

RUN adduser --disabled-password --gecos '' ctf

# enable 32-bit support
RUN dpkg --add-architecture i386
RUN apt update
RUN apt install -y libc6:i386 libstdc++6:i386
RUN apt install -y python3

# install packages
RUN apt install -y socat

# copy service/flag files
COPY target.py /target.py

RUN chmod 755 /target.py

# use ctf user instead of root
USER ctf

# run socat
CMD ["socat", "-T60", "TCP-LISTEN:9999,reuseaddr,fork", "EXEC:timeout 60 /target.py"]
