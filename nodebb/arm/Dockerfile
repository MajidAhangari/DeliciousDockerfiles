#
# Dockerfile for nodebb-arm
#

FROM arm32v7/alpine:3
MAINTAINER EasyPi Software Foundation

ENV BB_VER=1.17.0
ENV BB_URL=https://github.com/NodeBB/NodeBB/archive/v$BB_VER.tar.gz
ENV BB_SOURCE=/usr/src/nodebb
ENV BB_CONTENT=/var/lib/nodebb

WORKDIR $BB_SOURCE
VOLUME $BB_CONTENT

RUN set -ex \
    && apk add -U bash \
                  icu \
                  imagemagick \
                  nodejs \
                  nodejs-npm \
                  openssl \
    && apk add -t TMP build-base \
                      curl \
                      git \
                      icu-dev \
                      openssl-dev \
                      python \
                      tar \
    && curl -sSL $BB_URL | tar xz --strip 1 \
    && ./nodebb setup \
    && apk del TMP \
    && rm -rf /tmp/npm* \
              /var/cache/apk/*

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 4567
CMD ["./nodebb", "start"]
