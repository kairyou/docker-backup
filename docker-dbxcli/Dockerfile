FROM alpine:3.5

ENV DBXCLI_VERSION v2.0.2

# MAINTAINER Leon.Xu ( http://github.com/kairyou/ )

# x509: failed to load system roots and no roots provided
RUN apk add --no-cache --virtual .build-deps ca-certificates

# fix: Go binary not found in path on Alpine (stackoverflow.com/a/35613430)
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

ADD https://github.com/dropbox/dbxcli/releases/download/${DBXCLI_VERSION}/dbxcli-linux-amd64 /usr/local/bin/dbxcli
RUN chmod 0755 /usr/local/bin/dbxcli \
  && mkdir -p /root/.config/dbxcli /backup
# RUN /usr/local/bin/dbxcli --help

# /root/.config/dbxcli/auth.json # Dropbox access token
WORKDIR /backup

# CMD ["dbxcli"]
ENTRYPOINT ["dbxcli"]
