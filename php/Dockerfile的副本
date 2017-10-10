FROM centos:7
MAINTAINER AT <terry.dawu@gmail.com>

ENV TZ "Asia/Shanghai"

COPY redis-3.0.0.tgz /tmp/redis-3.0.0.tgz
RUN yum -y update && \
    yum install -y gcc automake autoconf libtool make gcc-c++ vixie-cron  wget zlib php-devel php-pear httpd-devel  file openssl-devel sharutils zip  bash vim cyrus-sasl-devel libmemcached libmemcached-devel libyaml libyaml-devel unzip libvpx-devel openssl-devel ImageMagick-devel  autoconf  tar gcc libxml2-devel gd-devel libmcrypt-devel libmcrypt mcrypt mhash libmcrypt libmcrypt-devel libxml2 libxml2-devel bzip2 bzip2-devel curl curl-devel libjpeg libjpeg-devel libpng libpng-devel freetype-devel bison libtool-ltdl-devel net-tools && \
    yum clean all

#fix error: mcrypt.h not found
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm && \
    yum install -y libmcrypt-devel

RUN cd /tmp && \
  wget http://cn2.php.net/distributions/php-7.0.12.tar.gz && \
  tar xzf php-7.0.12.tar.gz && \
  cd /tmp/php-7.0.12 && \
  ./configure \
    --prefix=/usr/local/php \
    --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir --enable-simplexml --enable-xml --disable-rpath --enable-bcmath --enable-soap --enable-zip --with-curl --enable-fpm --with-fpm-user=nobody --with-fpm-group=nobody --enable-mbstring --enable-sockets --with-mcrypt --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-opcache && \
    make && \
    make install

RUN cd /tmp && \
    tar xzf redis-3.0.0.tgz && \
    cd /tmp/redis-3.0.0 && \
    /usr/local/php/bin/phpize  && \
    ./configure --with-php-config=/usr/local/php/bin/php-config && \
    make && \
    make install


ADD php-fpm.conf /usr/local/php/etc/php-fpm.conf 
ADD composer.phar /usr/local/bin/composer 
ADD php.ini /usr/local/php/etc/php.ini
    
RUN cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf


WORKDIR /www
RUN chmod 755 /usr/local/bin/composer

EXPOSE 9000

VOLUME ["/www"]


#配置php
RUN sed -i -e 's/listen = 127.0.0.1:9000/listen = 9000/' /usr/local/php/etc/php-fpm.d/www.conf

#启动php
ENTRYPOINT ["/usr/local/php/sbin/php-fpm", "-F", "-c", "/usr/local/php/etc/php.ini"]





