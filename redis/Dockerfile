FROM centos:7
MAINTAINER AT <terry.dawu@gmail.com>


RUN yum -y install epel-release && \
    yum -y update

RUN    yum install -y gcc automake autoconf libtool make gcc-c++ vixie-cron  wget zlib  file openssl-devel  zip  bash vim cyrus-sasl-devel  libyaml libyaml-devel unzip libvpx-devel openssl-devel  gd-devel libmcrypt-devel libmcrypt mcrypt mhash libmcrypt libmcrypt-devel libxml2 libxml2-devel bzip2 bzip2-devel curl curl-devel  freetype-devel bison libtool-ltdl-devel net-tools && \
    yum clean all

RUN cd /tmp && \
  wget http://download.redis.io/releases/redis-3.2.6.tar.gz && \
  tar zxvf redis-3.2.6.tar.gz && \
  cd redis-3.2.6 && \
  make && \
  make install

ADD redis.conf /etc/redis.conf

EXPOSE 6379

VOLUME ["/data"]

WORKDIR /data

CMD "/usr/local/bin/redis-server" "/etc/redis.conf"
#ENTRYPOINT ["/usr/local/bin/redis-server", "-F", "-c", "/etc/redis.conf"] 
