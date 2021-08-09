FROM centos:7

RUN set -eux; \
    yum install -y yum-utils epel-release https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum-config-manager --disable epel

RUN set -eux; \
    yum install -y --enablerepo=epel,remi-php74 \
    zip \
    unzip \
    php \
    php-fpm \
    php-mbstring \
    php-pear \
    php-mcrypt \
    php-cli \
    php-common \
    php-json \
    php-mysqld \
    php-pdo \
    php-process \
    php-xml \
    php-pecl-mysql.x86_64 \
    php-devel \
    php-pecl-zip \
    php-gd \
    libwebp-devel \
    scl-utils \
    curl

# php-fpm setting
RUN mkdir /run/php-fpm
COPY php-fpm/www.conf /etc/php-fpm.d/www.conf
COPY php.ini /usr/local/etc/php/conf.d/php.ini

# change html dir permission for web server access
RUN chown -R apache:apache /var/www/html

# php composer install
COPY --from=composer /usr/bin/composer /usr/bin/composer

# nodejs and npm install
RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
RUN yum install -y nodejs

# change default dir
WORKDIR /var/www/html

# execute php-fpm foreground
ENTRYPOINT ["/usr/sbin/php-fpm", "-F"]

# execute following command
# docker-compose exec php composer install
# docker-compose exec php npm update -g
# docker-compose exec php npm install
# docker-compose exec php npm run dev

