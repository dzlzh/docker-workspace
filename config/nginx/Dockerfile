ARG NGINX_VERSION
FROM nginx:${NGINX_VERSION}
LABEL maintainer="dzlzh <dzlzh@null.net>"

RUN ln -snf /use/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

WORKDIR /var/www/html
