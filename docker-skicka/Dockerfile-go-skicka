FROM golang:1-alpine

MAINTAINER Leon.Xu ( http://github.com/kairyou/ )

# https://github.com/google/skicka

RUN apk add --no-cache --virtual .build-deps git
RUN go get github.com/google/skicka
ADD skicka.config /root/.skicka.config
RUN chmod 600 /root/.skicka.config

RUN mkdir /backup
WORKDIR /backup

# CMD ["skicka"]
ENTRYPOINT ["skicka"]
