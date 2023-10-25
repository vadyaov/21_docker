# Ubuntu 20.04
FROM ubuntu:20.04

ENV DOCKER_CONTENT_TRUST=1
ENV DEBIAN_FRONTEND noninteractive

# Update package and install stuff
RUN apt-get update && apt-get install -y \
  build-essential \
  libfcgi-dev \
  spawn-fcgi \
  nginx \
&& rm -rf /var/lib/apt/lists/*



RUN useradd -m aboba
USER aboba

# Copy server source
COPY ./server/fcgi_server.c app/

WORKDIR /app
USER root
RUN gcc -o hello_fcgi fcgi_server.c -lfcgi
USER aboba

COPY ./nginx/nginx.conf /etc/nginx/conf.d

HEALTHCHECK --interval=30s --timeout=10s --retries=3 CMD curl --fail http://localhost:8080 || exit 1

ENTRYPOINT ["/bin/bash", "-c", "spawn-fcgi -p 8080 ./hello_fcgi; nginx -g 'daemon off;'"]
