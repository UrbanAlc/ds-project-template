FROM centos:centos8

# CentOS deposunu güncelle ve gerekli paketleri kur
RUN yum update -y && \
    yum install -y sudo python3.9 python3-pip

# Development Tools grubunu kur
RUN yum groupinstall "Development Tools" -y

# Python pip'i güncelle
RUN pip3 install --upgrade pip

# Gerekli kütüphaneleri kopyala ve yükle
COPY src/ /{{cookiecutter.project_slug}}/src
COPY data/ /{{cookiecutter.project_slug}}/data
COPY models/ /{{cookiecutter.project_slug}}/models
COPY ./requirements.txt /{{cookiecutter.project_slug}}
COPY ./ds_app.py /{{cookiecutter.project_slug}}

WORKDIR /{{cookiecutter.project_slug}}

# Python sürümünü 3.11'e yükselt
RUN alternatives --set python /usr/bin/python3.11

# Python kütüphanelerini yükle
RUN pip3 install -r requirements.txt
