FROM nginx:stable-alpine

LABEL maintainer="Tuan Ha <tuanht.unix@gmail.com>"

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf

WORKDIR /var/www
