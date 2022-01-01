FROM bwalia/openresty119php74:latest

COPY kisaan.com-devops/docker/php/php.ini /usr/local/etc/php/php.ini
COPY kisaan.com-devops/docker/nginx/nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

# # setup nginx log file dir path /var/log/nginx/
RUN mkdir -p /var/log/nginx/
RUN chgrp www-data -R /var/log/nginx/
RUN mkdir -p /var/nginx/
RUN chmod 777 -R /var/nginx/
RUN chgrp www-data -R /var/nginx/
# RUN touch /var/nginx/nginx.pid
# RUN mkdir -p /var/run/php-fpm/
# RUN chmod 777 -R /var/run/php-fpm/

# Setup website frontend
RUN mkdir -p /var/www/html/kisaan.com

#RUN mkdir -p /var/www/html/kisaan.com
COPY kisaan.com /var/www/html/kisaan.com/

RUN chgrp www-data -R /var/www/html/
RUN chmod 777 -R /var/www/html/
#RUN mv /var/www/html/env /var/www/html/.env

RUN chgrp www-data -R /var/www/html/kisaan.com/
RUN chmod 777 -R /var/www/html/kisaan.com/

RUN mkdir -p /var/php
RUN apk add supervisor

COPY kisaan.com-devops/docker/openresty-php/supervisord.conf /etc/

ENTRYPOINT /usr/bin/supervisord -c /etc/supervisord.conf

STOPSIGNAL SIGQUIT