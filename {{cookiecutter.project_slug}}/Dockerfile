FROM centos:centos8

RUN cd /etc/yum.repos.d/ \
    && sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
    && sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN yum update -y \
    && yum install sudo -y \
    && yum groupinstall "Development Tools" -y \
    && yum install wget -y

# Python 3.10'u derle ve yükle
RUN cd /tmp \
    && wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz \
    && tar -xf Python-3.10.0.tgz \
    && cd Python-3.10.0 \
    && ./configure \
    && make \
    && make install

# Python 3.10 için pip'i yükle
RUN wget https://bootstrap.pypa.io/get-pip.py \
    && python3.10 get-pip.py \
    && rm -f get-pip.py

COPY src/ /{{cookiecutter.project_slug}}/src
COPY data/ /{{cookiecutter.project_slug}}/data
COPY models/ /{{cookiecutter.project_slug}}/models
COPY ./requirements.txt /{{cookiecutter.project_slug}}
COPY ./ds_app.py /{{cookiecutter.project_slug}}

WORKDIR /{{cookiecutter.project_slug}}

# Python bağımlılıklarını yükle
RUN pip3.10 install -r requirements.txt
