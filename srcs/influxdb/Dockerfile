FROM alpine:3.12
EXPOSE 8086
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk update
RUN apk add openrc influxdb telegraf
RUN openrc && touch /run/openrc/softlevel
VOLUME [ "/var/lib/influxdb" ]
COPY ./telegraf.conf /etc/
COPY start-influxdb.sh .
COPY probe.sh /
ENTRYPOINT sh start-influxdb.sh