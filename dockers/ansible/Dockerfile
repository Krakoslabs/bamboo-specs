FROM ubuntu:bionic

LABEL maintainer="@krakoslabs"

ENV DEBIAN_FRONTEND noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apt-utils \
    software-properties-common \
    build-essential \
    jq \
    git \
    python3 \
    python3-dev \
    python3-pip && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade \
    setuptools \
    pip

ADD requirements.txt /requirements.txt

RUN pip3 install --upgrade -r /requirements.txt

RUN ln -s /usr/bin/python3 /usr/bin/python

RUN groupadd -g 1001 ansible && \
    useradd -r -u 1001 -g ansible ansible

RUN mkdir /home/ansible
RUN chown -R ansible:ansible /home/ansible

USER ansible

WORKDIR /home/ansible
