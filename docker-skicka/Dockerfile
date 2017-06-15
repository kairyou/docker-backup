FROM alpine:3.5

MAINTAINER Leon.Xu ( http://github.com/kairyou/ )

# https://github.com/google/skicka

# fix x509: failed to load system roots and no roots provided
RUN apk add --no-cache --virtual .build-deps ca-certificates

ADD skicka /bin/skicka
ADD skicka.config /root/.skicka.config
RUN chmod 600 /root/.skicka.config \
  && mkdir /backup
  
WORKDIR /backup

# CMD ["skicka"]
ENTRYPOINT ["skicka"]
