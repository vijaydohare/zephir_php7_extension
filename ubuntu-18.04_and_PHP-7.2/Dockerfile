# Download base image ubuntu 18.04
FROM ubuntu:18.04

ENV TZ=Etc/UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone && \
    \
    apt-get update && \
    apt-get install -y \
    git \
    gcc \
    make \
    re2c \
    php \
    php-json \
    php-dev \
    php-zip \
    php-mbstring \
    libpcre3-dev \
    unzip \
    wget \
    curl \
    vim \
    build-essential && \
    \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    \
    HASH="$(wget -q -O - https://composer.github.io/installer.sig)" && \
    \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    \
    composer && \
    \
    composer global require phalcon/zephir && \
    \
    composer global install && \
    \
    ln -s /root/.composer/vendor/bin/zephir /usr/local/bin && \
    \
    zephir list && \
    \
    git clone git://github.com/phalcon/php-zephir-parser.git && \
    \
    cd php-zephir-parser && /usr/bin/phpize && ./configure --with-php-config=/usr/bin/php-config && \
    \
    make && make install

ADD 20-zephir_parser.ini /etc/php/7.2/cli/conf.d/20-zephir_parser.ini


# Configure Services
ADD start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]
