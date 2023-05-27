FROM debian:bullseye

RUN apt-get update \
 && apt-get install -y --no-install-recommends systemd bash python3 sudo \
 && rm -rf /var/lib/apt/lists

RUN /bin/bash -c 'echo "root:123qwe" | chpasswd'

COPY autologin.conf /lib/systemd/system/console-getty.service

ENTRYPOINT ["/lib/systemd/systemd"]
