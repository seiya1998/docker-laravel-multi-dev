FROM php:7.3-fpm
EXPOSE 5173
RUN apt-get update \
  && apt-get -y install \
    git \
    zip \
    unzip \
  && docker-php-ext-install pdo_mysql mysqli bcmath mbstring

# composer インストール
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# Node インストール
ENV NODE_VERSION=14.15.5
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
ENV NVM_DIR=/root/.nvm
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
RUN node --version
RUN npm --version

WORKDIR /src
ADD . /src/storage
RUN chown -R www-data:www-data /src/storage