FROM alpine:3.12
EXPOSE 80 443 22
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk update
RUN apk add nginx openssl openssh openrc telegraf && mkdir /run/nginx/;
RUN mkdir .ssh
RUN adduser -D admin -G root && echo "admin:admin" | chpasswd
RUN echo "<h1>Nginx page.</h1>" > /var/www/localhost/htdocs/index.html;
RUN openssl req -x509 -nodes -days 10 -subj "/C=RU/ST=Tatarstan/O=School 21/CN=localhost" \
-addext "subjectAltName=DNS:localhost" \
-newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key \
-out /etc/ssl/certs/nginx-selfsigned.crt
COPY default.conf /etc/nginx/conf.d
COPY authorized_keys .ssh/
COPY ./telegraf.conf /etc/
COPY start-nginx.sh .
COPY probe.sh /
RUN chown -R admin:root /etc/ssh
ENTRYPOINT sh start-nginx.sh