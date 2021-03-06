FROM centos:7.4.1708 

# Install base soft
RUN yum install -y epel-release
RUN set -x \
    && yum install -y wget git gcc make cmake gcc-c++ bison-devel ncurses-devel zlib-devel gd-devel curl-devel libxml2-devel libicu-devel libcurl-devel libicu-devel libevent-devel bzip2-devel libtidy-devel libjpeg-turbo-devel libpng-devel openssl-devel openldap-devel freetype-devel libmcrypt-devel tzdata ImageMagick-devel m4 autoconf librdkafka-devel \
    && yum clean all \
    && rm -rf /var/cache/yum/

# Work directory
WORKDIR /data/service

# Install Mysql module version=5.6.27
RUN set -x \
    && wget -c http://mirror.neu.edu.cn/mysql/Downloads/MySQL-5.6/mysql-5.6.27.tar.gz \
    && tar zxvf mysql-5.6.27.tar.gz \
    && cd mysql-5.6.27 \
    && cmake -DCMAKE_INSTALL_PREFIX=/data/service/mysql \
    && make -j 4 \
    && make install \
    && rm -rf ../mysql-*

# Global enviroment
ENV LD_LIBRARY_PATH=/data/service/mysql/lib:/lib/:/usr/lib/:/usr/local/lib
ENV PATH=/data/service/php7.0.16/sbin:/data/service/php7.0.16/bin:$PATH
ENV TZ=Asia/Shanghai

# Install Php version=7.0.16
RUN set -x \
    && wget -c http://ftp.ntu.edu.tw/php/distributions/php-7.0.16.tar.gz \
    && tar zxvf php-7.0.16.tar.gz \
    && cd php-7.0.16 \
    && ./configure --prefix=/data/service/php7.0.16 --with-config-file-path=/data/service/php7.0.16/etc --enable-fpm --with-fpm-user=www --with-fpm-group=www --enable-mysqlnd --enable-mysqlnd-compression-support --enable-calendar --enable-exif --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl --enable-mbregex --enable-mbstring --enable-intl  --with-libmbfl --enable-ftp --with-gd --enable-gd-jis-conv --with-openssl --with-mhash --enable-pcntl --enable-sockets --enable-wddx --with-tidy --with-xmlrpc --with-kerberos --with-libdir=lib64 --enable-zip --enable-soap --with-gettext --with-mcrypt --enable-opcache --with-pear --enable-maintainer-zts --with-ldap=shared --without-gdbm --with-pcre-dir --with-pdo-mysql=/data/service/mysql --with-mysqli=/data/service/mysql/bin/mysql_config \
   && make -j 4 \
   && make install \
   && rm -rf ../php-*

# Install libmemcached version=1.0.18
RUN set -x \
    && wget -c https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz \
    && tar zxvf libmemcached-1.0.18.tar.gz \
    && cd libmemcached-1.0.18 \
    && ./configure --prefix=/data/service/libmemcached \
    && make -j 4 \
    && make install \
    && rm -rf ../libmemcached-*

# Install memcached moudule version=3.1.3
RUN set -x \
    && curl -O https://pecl.php.net/get/memcached-3.1.3.tgz \
    && tar zxvf memcached-3.1.3.tgz \
    && cd memcached-3.1.3 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config  -with-libmemcached-dir=/data/service/libmemcached  --disable-memcached-sasl \
    && make -j 4 \
    && make install \
    && rm -rf ../memcached-*

# Install memcache module version=4.0.3
RUN set -x \
    && git clone https://github.com/websupport-sk/pecl-memcache \
    && cd pecl-memcache \
    && git checkout 4.0.3 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../pecl-memcache

# Install Redis module version=3.1.1
RUN set -x \
    && wget -c https://pecl.php.net/get/redis-3.1.1RC2.tgz \
    && tar zxvf redis-3.1.1RC2.tgz \
    && cd redis-3.1.1RC2 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../redis-*

# Install apcu module version=5.1.8
RUN set -x \
    && wget -c https://pecl.php.net/get/apcu-5.1.8.tgz \
    && tar zxvf apcu-5.1.8.tgz \
    && cd apcu-5.1.8 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../apcu-*

#Install imagick module version=3.4.4
RUN set -x \
    && wget -c https://pecl.php.net/get/imagick-3.4.4.tgz \
    && tar zxvf imagick-3.4.4.tgz \
    && cd imagick-3.4.4 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../imagick-*

# Install mongodb module version=1.2.5
RUN set -x \
    && wget -c https://pecl.php.net/get/mongodb-1.2.5.tgz \
    && tar zxvf mongodb-1.2.5.tgz \
    && cd mongodb-1.2.5 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../mongodb-*

# Install rdkafka module version=3.0.1
RUN set -x \
    && wget -c https://pecl.php.net/get/rdkafka-3.0.1.tgz \
    && tar zxvf rdkafka-3.0.1.tgz \
    && cd rdkafka-3.0.1 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../rdkafka-*

# Install grpc module version=1.20.0
RUN set -x \
    && wget -c https://pecl.php.net/get/grpc-1.16.0.tgz \
    && tar zxvf grpc-1.16.0.tgz \
    && cd grpc-1.16.0 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../grpc-*

# Install phpng-xhprof module version=0.9.5
RUN set -x \
    && git clone http://www.github.com/yaoguais/phpng-xhprof \
    && cd phpng-xhprof \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf ../phpng-xhprof

# Install thrift_protocol module version=1.0
RUN set -x \
    && wget -c https://github.com/apache/thrift/archive/0.10.0.tar.gz \
    && tar zxvf 0.10.0.tar.gz \
    && cd thrift-0.10.0/lib/php/src/ext/thrift_protocol \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf /data/service/{0.10.0.tar.gz,thrift-0.10.0}

# Install tideways module version=4.1.6
RUN set -x \
    && git clone https://github.com/tideways/php-xhprof-extension.git \
    && cd php-xhprof-extension \
    && git checkout v4.1.6 \
    && phpize \
    && ./configure --with-php-config=/data/service/php7.0.16/bin/php-config \
    && make -j 4 \
    && make install \
    && rm -rf /data/service/php-xhprof-extension

# Install  doumo_dek
# set ssh-key
COPY config id_rsa id_rsa.pub /root/.ssh/
RUN chmod 0600 /root/.ssh/id_rsa*

# Add user uid=gid=500
RUN set x \
    && groupadd -g 500 www \
    && adduser -u 500 -g www www

# Create base directory
RUN mkdir -p /data/service_logs/php_log

# Copy config file
COPY php.ini php-fpm.conf /data/service/php7.0.16/etc/
COPY www.conf /data/service/php7.0.16/etc/php-fpm.d/

# Run service
CMD ["php-fpm","-F"]
