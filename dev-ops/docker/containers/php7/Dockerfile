FROM webdevops/php-apache-dev:7.4

# https://dockerfile.readthedocs.io/en/latest/content/DockerImages/dockerfiles/php-apache-dev.html#composer
ENV COMPOSER_VERSION=2
ENV COMPOSER_HOME=/.composer
ENV WEB_DOCUMENT_ROOT=/var/www/shopware/shopware

COPY wait-for-it.sh /usr/local/bin/
COPY php-config.ini /usr/local/etc/php/conf.d/
COPY xdebug.ini /usr/local/etc/php/conf.d/
COPY createuser.sh /addExternalUser
RUN chmod +rwx /addExternalUser
RUN /addExternalUser

# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN mkdir -p /usr/share/man/man1

RUN apt-get update && apt-get install -y ant default-mysql-client

RUN chmod +x /usr/local/bin/wait-for-it.sh \
&& ln -s /app/psh.phar /bin/psh

WORKDIR /var/www/shopware
