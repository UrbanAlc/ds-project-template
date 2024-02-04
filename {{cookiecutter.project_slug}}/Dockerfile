FROM centos:centos8

RUN cd /etc/yum.repos.d/ \
    && sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
    && sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN yum update -y \
    && yum install sudo -y \
    && yum groupinstall "Development Tools" -y

# Python 3.10'u yükle
RUN yum install -y https://centos.pkgs.org/8/centos-power-tools-aarch64/python39-3.9.7-1.el8.aarch64.rpm
RUN yum install -y https://centos.pkgs.org/8/centos-baseos-aarch64/python39-pip-20.3.4-1.el8.noarch.rpm

# Python 3.10 için pip'i güncelle
RUN python3.10 -m pip install --upgrade pip

COPY src/ /{{cookiecutter.project_slug}}/src
COPY data/ /{{cookiecutter.project_slug}}/data
COPY models/ /{{cookiecutter.project_slug}}/models
COPY ./requirements.txt /{{cookiecutter.project_slug}}
COPY ./ds_app.py /{{cookiecutter.project_slug}}

WORKDIR /{{cookiecutter.project_slug}}

RUN pip3.10 install -r requirements.txt
