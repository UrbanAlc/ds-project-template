# Resmi CentOS imajını kullan
FROM centos:latest

# Repository konfigürasyonunu vault.centos.org mirro'su kullanacak şekilde güncelle
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* && \
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

# Konteynerdeki çalışma dizinini belirle
WORKDIR /app

# Repoları güncelle ve gerekli bağımlılıkları yükle
RUN yum update -y && \
    yum install -y openssl-devel bzip2-devel libffi-devel wget && \
    yum groupinstall -y "Development Tools"

# Python 3.10.2 indir ve kur
RUN wget https://www.python.org/ftp/python/3.10.2/Python-3.10.2.tgz && \
    tar -xzf Python-3.10.2.tgz && \
    cd Python-3.10.2 && \
    ./configure --enable-optimizations && \
    make altinstall

# Varsayılan Python sürümünü ayarla
RUN ln -s /usr/local/bin/python3.10 /usr/local/bin/python

# Pip'i kur ve yolu ayarla
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python get-pip.py && \
    rm get-pip.py

# Base imajda dahil edilmemişse wget'i yükle
RUN yum install -y wget && yum clean all

# Konteyner başladığında çalışacak komutu belirt
RUN python --version && \
    pip3 --version
