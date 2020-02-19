FROM node:8-alpine

MAINTAINER Cameron Carney <ccarney16@live.com>

ARG VERSION

ENV DAEMON_VERSION="v0.6.12" \
    UID=500

WORKDIR /srv/daemon

RUN \
 apk --update --no-cache add coreutils curl openssl make gcc g++ python gnupg tar \
 && curl -Lo daemon.tar.gz https://github.com/Pterodactyl/Daemon/archive/${DAEMON_VERSION}.tar.gz \
 && tar --strip-components=1 -xzvf daemon.tar.gz \
 && rm -f daemon.tar.gz \
 && npm install --production \
 && npm install --save node_extra_ca_certs_mozilla_bundle \
 && addgroup -S -g ${UID} pterodactyl && adduser -S -D -H -G pterodactyl -u ${UID} -s /bin/false pterodactyl \
 && apk del curl make gcc g++ python gnupg \
 && rm -rf /root/.npm /root/.node-gyp /root/.gnupg \
 /var/cache/apk/* /tmp/*

EXPOSE 8080

CMD [ "NODE_EXTRA_CA_CERTS=node_modules/node_extra_ca_certs_mozilla_bundle/ca_bundle/ca_intermediate_root_bundle.pem", "npm", "start" ]
