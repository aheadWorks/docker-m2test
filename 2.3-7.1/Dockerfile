#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "update.py"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
ARG BASE_VERSION="7.1"
FROM aheadworks/phpdev:${BASE_VERSION}

ARG EDITION="community"
ARG MAGENTO_VERSION="2.3.2"

ARG COMPOSER_AUTH

RUN pip3 install click \
    && cd /tmp \
    && curl https://codeload.github.com/magento/magento2/tar.gz/$MAGENTO_VERSION -o $MAGENTO_VERSION.tar.gz \
    && tar xvfp $MAGENTO_VERSION.tar.gz \
    && mv magento2-$MAGENTO_VERSION/* magento2-$MAGENTO_VERSION/.htaccess /var/www/html \
    && cd /var/www/html \
    && composer config repositories.magento composer https://repo.magento.com/ \
    && chmod u+x bin/magento \
    && composer install \
    && composer create-project magento/magento-coding-standard --stability=dev /magento-coding-standard \
    && cd /tmp \
    && cd /var/www/html && composer config --unset repositories.magento


COPY m2test.py /m2test.py
COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["ash", "/entrypoint.sh"]


