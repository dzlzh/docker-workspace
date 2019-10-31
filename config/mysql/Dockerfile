ARG MYSQL_VERSION
FROM mysql:${MYSQL_VERSION}
LABEL maintainer="dzlzh <dzlzh@null.net>"

RUN ln -snf /use/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone
