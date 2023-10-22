# Ubuntu 22.04
FROM ubuntu:22.04

# Update package and install stuff
RUN apt-get update && apt-get install -y \
  build-essential \
  libfcgi-dev \
  spawn-fcgi \
  nginx

# Copy server source
COPY ./server/ app/

WORKDIR /app
RUN gcc -o hello_fcgi fcgi_server.c -lfcgi
RUN chmod +x ./run_server.sh
CMD ./run_server.sh

RUN ls /etc/nginx/conf.d
COPY ./nginx/nginx.conf /etc/nginx/conf.d/
CMD nginx -g 'daemon off;'

