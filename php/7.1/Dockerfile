FROM php:7.1

LABEL maintainer "Eduardo Bizarro <eduardo@zendev.com.br>" \
      php="7.1" \
      node="8"

# Set correct environment variables
ENV IMAGE_USER=php
ENV HOME=/home/$IMAGE_USER
ENV COMPOSER_HOME=$HOME/.composer
ENV PATH=$HOME/.yarn/bin:$PATH

WORKDIR /tmp

# COPY INSTALL SCRIPTS
COPY ./php/scripts/*.sh /tmp/
RUN chmod +x /tmp/*.sh

# Install
RUN bash ./packages.sh \
    && bash ./extensions.sh \
    && bash ./composer.sh \
    && bash ./node.sh \
    && bash ./cleanup.sh

RUN adduser --disabled-password --gecos "" $IMAGE_USER && \
    echo "$IMAGE_USER  ALL = ( ALL ) NOPASSWD: ALL" >> /etc/sudoers && \
    mkdir -p /var/www/html && \
    chown -R $IMAGE_USER:$IMAGE_USER /var/www

RUN chown -R $IMAGE_USER:$IMAGE_USER $HOME

USER $IMAGE_USER

WORKDIR /var/www/html
