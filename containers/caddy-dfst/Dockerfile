FROM alpine:3.2
MAINTAINER Eliot Kimber <ekimber@contrext.com>
# See e.g., https://hub.docker.com/r/abiosoft/caddy/ for 

LABEL caddy_version="0.9.5" architecture="amd64"

RUN apk add --update openssh-client git tar

RUN curl --silent --show-error --fail --location \
      --header "Accept: application/tar+gzip, application/x-gzip, application/octet-stream" -o - \
      "https://caddyserver.com/download/build?os=linux&arch=amd64&features=git,search" \
    | tar --no-same-owner -C /usr/bin/ -xz caddy \
 && chmod 0755 /usr/bin/caddy \
 && /usr/bin/caddy -version

EXPOSE 80 443 2015
VOLUME /srv/www
WORKDIR /srv/www

ADD Caddyfile /etc/Caddyfile
ADD index.html /srv/www/index.html

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["--conf", "/etc/Caddyfile"]