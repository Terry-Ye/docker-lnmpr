FROM centos:7
MAINTAINER AT <terry.dawu@gmail.com>

ENV TZ "Asia/Shanghai"


RUN yum -y install epel-release && \
    yum -y update 

RUN    yum install -y gcc automake autoconf libtool make gcc-c++ vixie-cron  wget zlib  file openssl-devel sharutils zip  bash vim cyrus-sasl-devel libmemcached libmemcached-devel libyaml libyaml-devel unzip libvpx-devel openssl-devel ImageMagick-devel  autoconf  tar gcc libxml2-devel gd-devel libmcrypt-devel libmcrypt mcrypt mhash libmcrypt libmcrypt-devel libxml2 libxml2-devel bzip2 bzip2-devel curl curl-devel libjpeg libjpeg-devel libpng libpng-devel freetype-devel bison libtool-ltdl-devel net-tools && \
    yum clean all
#Nginx
RUN cd /tmp && \
  wget http://nginx.org/download/nginx-1.12.1.tar.gz && \
  tar xzf nginx-1.12.1.tar.gz && \
  cd /tmp/nginx-1.12.1 && \
  ./configure \
    --prefix=/usr/local/nginx \
    --with-http_ssl_module --with-http_sub_module --with-http_dav_module --with-http_flv_module \
    --with-http_gzip_static_module --with-http_stub_status_module --with-debug && \
    make && \
    make install

ADD nginx.conf /usr/local/nginx/conf/nginx.conf
ADD vhost/* /usr/local/nginx/conf/vhost/


EXPOSE 80 443
#启动nginx
ENTRYPOINT ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
