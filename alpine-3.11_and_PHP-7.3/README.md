# zephir_php7_extension - alpine-3.11_and_PHP-7.3

After downloading the "Dockerfile" and "00_zephir_parser.ini", Please execute following command in the same directory where all these files exists

#### To build the docker image
    docker build -t php_ext_alpine .

#### After successfull build start the container
    docker run -d --name php-extension-alpine --log-opt max-size=10m --log-opt max-file=3 php_ext_alpine

#### Login to newly created docker container
    docker exec -it php-extension-alpine bash

#### Inside container move to the home directory (we can use any other directory)
    cd ~

#### Initialize the extension project
    zephir init helloworld

#### Move into the directory created by the above command
    cd helloworld

#### Create and open a file in vim editor
    vim helloworld/greeting.zep

Inside the file put following code

    namespace HelloWorld;

    class Greeting
    {
        public static function say()
        {
            echo "Hello World!";
        }
    }

save and close the file

#### Compile and build
    zephir build

#### if everthing goes perfect then we can find a file created in the "~/helloworld/ext/modules" directory, then we can copy the file to php extension directory
    cp ext/modules/helloworld.so  /usr/lib/php7/modules/

#### To enable this extension we need to create a new file at the following location (we can use the default php.ini file also)
    vim /etc/php7/conf.d/helloworld.ini

Inside the file put following line

    extension=helloworld.so;

save and close the file

#### Restart PHP
    kill -USR2 1

#### Time to test our extension
     vim zephir_helloworld.php

Inside the file put following code

    <?php
    echo HelloWorld\Greeting::say()."\n";

save and close the file

#### Finally test the PHP code with the extension
    php zephir_helloworld.php




### Reference
Special thanks for such a nice article - https://medium.com/tech-tajawal/introduction-to-php7-extension-cd802b8ecc1c

