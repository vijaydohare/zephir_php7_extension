# Download base image alpine 3.11
FROM alpine:3.11

RUN apk update

RUN apk add --no-cache build-base git gcc make unzip wget curl re2c php7 php7-dev php7-json php7-zip php7-mbstring php7-openssl php7-phar php7-ctype php7-xml php7-dom php7-tokenizer libpcre32 vim
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN HASH="$(wget -q -O - https://composer.github.io/installer.sig)"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN composer
RUN composer global require phalcon/zephir
RUN composer global install
RUN ln -s /root/.composer/vendor/bin/zephir /usr/local/bin
RUN zephir list
RUN git clone git://github.com/phalcon/php-zephir-parser.git
RUN cd php-zephir-parser && /usr/bin/phpize && ./configure --with-php-config=/usr/bin/php-config && make && make install
RUN rm -rf php-zephir-parser
RUN apk del git gcc make unzip wget curl

ADD 00_zephir_parser.ini /etc/php7/conf.d/00_zephir_parser.ini


CMD ["tail", "-f", "/etc/issue"]
