# Ubuntu 22.04
FROM ubuntu:22.04

# Update package and install stuff
RUN apt-get update && apt-get install -y \
  build-essential \
  libfcgi-dev \
  spawn-fcgi \
  nginx

# Copy server source
RUN mkdir /app
COPY ./server/fcgi_server.c app/

WORKDIR /app
RUN gcc -o hello_fcgi fcgi_server.c -lfcgi

COPY ./nginx/nginx.conf /etc/nginx/conf.d

ENTRYPOINT ["/bin/bash", "-c", "spawn-fcgi -p 8080 ./hello_fcgi; nginx -g 'daemon off;'"]
