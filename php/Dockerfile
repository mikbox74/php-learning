FROM php:8.0.0-fpm-alpine

ARG USER_ID
ARG GROUP_ID

RUN echo http://dl-2.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories
RUN apk --no-cache add shadow

RUN mkdir -p /usr/local/php-logs

######## [PHP Modules] Default ########
#### Core
#### ctype
#### curl
#### date
#### dom
#### fileinfo
#### filter
#### ftp
#### hash
#### iconv
#### json
#### libxml
#### mbstring
#### mysqlnd
#### openssl
#### pcre
#### PDO
#### pdo_sqlite
#### Phar
#### posix
#### readline
#### Reflection
#### session
#### SimpleXML
#### sodium
#### SPL
#### sqlite3
#### standard
#### tokenizer
#### xml
#### xmlreader
#### xmlwriter
#### zlib

######## Composer.phar ########
RUN curl -s https://getcomposer.org/installer | php \
  # move composer into a bin directory you control:
  && mv composer.phar /usr/local/bin/composer \
  # double check composer works
  && composer about

RUN php -m && echo "============================================="

######## Dependencies ########
#### bzip2-dev: bz2
#### enchant2-dev: enchant
#### gd: libpng-dev
#### gmp: gmp-dev
#### imap: imap-dev
#### intl: icu-dev
#### ldap: openldap-dev
#### pdo_dblib: freetds-dev
#### pdo_pgsql: postgresql-dev
#### pgsql: postgresql-dev
#### pspell: aspell-dev
#### snmp: net-snmp-dev
#### soap: libxml2-dev
#### tidy: tidyhtml-dev
#### xsl: libxslt-dev
#### zip: libzip-dev

RUN apk add --no-cache --update \
  bzip2-dev \
  enchant2-dev \
  libpng-dev \
  gmp-dev \
  imap-dev \
  icu-dev \
  openldap-dev \
  freetds-dev \
  postgresql-dev \
  aspell-dev \
  net-snmp-dev \
  libxml2-dev \
  tidyhtml-dev  \
  libxslt-dev \
  libzip-dev

RUN docker-php-ext-install \
  bcmath \
  bz2 \
  calendar \
  dba \
  enchant \
  exif \
  ffi \
  gd \
  gettext \
  gmp \
  imap \
  intl \
  ldap \
  mysqli \
  opcache \
  pcntl \
  pdo_dblib \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  pspell \
  shmop \
  snmp \
  soap \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm \
  tidy \
  xsl \
  zend_test \
  zip

######## PHP MODULES not working yet ########
#### oci8
#### odbc
#### pdo_firebird
#### pdo_oci
#### pdo_odbc

COPY ./php.ini /usr/local/etc/php/php.ini

RUN rm -rf /tmp/* /var/cache/apk/* \
  && echo "=============================================" \
  && php -m

RUN usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

# Starting
CMD chown -R www-data:www-data /var/app && \
  touch /usr/local/php-logs/php-fpm.log && \
  chmod 666 /usr/local/php-logs/php-fpm.log && \
  php-fpm -F

EXPOSE 9000