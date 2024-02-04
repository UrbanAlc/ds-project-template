FROM centos:centos8

# CentOS deposunu güncelle ve gerekli paketleri kur
RUN yum update -y && \
    yum install -y sudo

# Development Tools grubunu kur
RUN yum groupinstall "Development Tools" -y

# Python 3.11'i indir ve kur
RUN yum install -y python3.11 python3.11-devel

# Alternatives ile Python sürümünü ayarla
RUN alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1

# Python pip'i güncelle
RUN python3.11 -m ensurepip --default-pip && \
    ln -s /usr/bin/pip3.11 /usr/bin/pip

# Gerekli kütüphaneleri kopyala ve yükle
COPY src/ /{{cookiecutter.project_slug}}/src
COPY data/ /{{cookiecutter.project_slug}}/data
COPY models/ /{{cookiecutter.project_slug}}/models
COPY ./requirements.txt /{{cookiecutter.project_slug}}
COPY ./ds_app.py /{{cookiecutter.project_slug}}

WORKDIR /{{cookiecutter.project_slug}}

# Python kütüphanelerini yükle
RUN pip install --upgrade pip && \
    pip install -r requirements.txt
