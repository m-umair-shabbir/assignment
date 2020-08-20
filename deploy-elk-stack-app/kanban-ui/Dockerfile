### STAGE 1: Build ###
FROM node:12.7-alpine AS build
WORKDIR /usr/src/app
COPY package.json ./
RUN npm install
COPY . .
RUN npm run build

### STAGE 2: Run ###
FROM openjdk:8-alpine
RUN mkdir -p /usr/share/nginx/html
COPY --from=build /usr/src/app/dist/kanban-ui /usr/share/nginx/html

RUN apk upgrade

RUN apk --no-cache add supervisor \
                     nginx \
                     curl \
                     bash &&\
        curl -Ls https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.21-r2/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk &&\
        apk add --allow-untrusted /tmp/glibc-2.21-r2.apk

ADD https://artifacts.elastic.co/downloads/logstash/logstash-7.9.0.tar.gz /usr/share/
RUN tar -zxvf /usr/share/logstash-7.9.0.tar.gz -C /usr/share/
COPY default.conf /etc/nginx/conf.d/default.conf
COPY test.conf /test.conf
COPY supervisord-nginx-logstash.ini /etc/supervisord.d/supervisord-nginx-logstash.ini
COPY supervisord.conf /etc/supervisord.conf

RUN mkdir -p /var/log/supervisor \
    mkdir -p /run/nginx/ && \
    touch /run/nginx/nginx.pid \
    chmod +x /etc/supervisord.conf \
    chmod +x /usr/share/logstash-7.9.0/bin/logstash

EXPOSE 80

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
