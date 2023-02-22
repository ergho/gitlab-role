FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apt-utils \
    build-essential \
    locales \
    python3-dev \
    python3-setuptools \
    python3-pip \
    python3-yaml \
    sudo systemd iproute2\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/share/doc && rm -rf /usr/share/man

RUN locale-gen en_US.UTF-8

RUN python3 -m pip install ansible

RUN mkdir -p /etc/ansible

RUN echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

VOLUME ["/sys/fs/cgroup", "/tmp", "/run"]

CMD ["/lib/systemd/systemd"]
