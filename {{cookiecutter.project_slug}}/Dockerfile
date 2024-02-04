FROM centos:centos8

RUN cd /etc/yum.repos.d/ \
    && sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
    && sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN yum update -y \
    && yum install sudo -y \
    && yum groupinstall "Development Tools" -y \
    && yum install python3.10 -y \
    && alternatives --set python /usr/bin/python3.10 \
    && alternatives --set python3 /usr/bin/python3.10 \
    && yum install python3.10-pip -y

COPY src/ /{{cookiecutter.project_slug}}/src
COPY data/ /{{cookiecutter.project_slug}}/data
COPY models/ /{{cookiecutter.project_slug}}/models
COPY ./requirements.txt /{{cookiecutter.project_slug}}
COPY ./ds_app.py /{{cookiecutter.project_slug}}

WORKDIR /{{cookiecutter.project_slug}}

RUN pip3.10 install -r requirements.txt
