FROM 123154119074.dkr.ecr.eu-west-2.amazonaws.com/tenthmatrix/openresty119php74:latest

COPY kisaan.com-devops/docker/php/php.ini /usr/local/etc/php/php.ini
COPY kisaan.com-devops/docker/nginx/nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

RUN mkdir -p /var/www/html/kisaan.com

# Setup website frontend

ADD kisaan.com /var/www/html/kisaan.com/

RUN chgrp www-data -R /var/www/html/kisaan.com/
RUN chmod 777 -R /var/www/html/kisaan.com/
#RUN chmod 777 -R /var/www/html/kisaan.com/writable/cache/
#RUN mv /var/www/html/marshallharber_website/env /var/www/html/marshallharber_website/.env

# Secrets are injected inflight so move them to the right place for code igniter
#COPY .marshallharber_website_env /var/www/html/marshallharber_website/.env
#COPY .marshallharber_admin_env /var/www/html/marshallharber_admin/.env

RUN mkdir -p /var/php
RUN apk add supervisor

COPY kisaan.com-devops/docker/openresty-php/supervisord.conf /etc/

ENTRYPOINT /usr/bin/supervisord -c /etc/supervisord.conf

STOPSIGNAL SIGQUIT

