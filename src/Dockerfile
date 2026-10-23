ARG ALPINE_VERSION=3.24.3
FROM alpine:${ALPINE_VERSION}
RUN apk upgrade --no-cache && apk add --no-cache bash sqlite restic
WORKDIR /app
COPY logging /app/logging
COPY file-env /app/file-env
COPY backup /app/backup
RUN chmod a+x /app/logging && chmod a+x /app/file-env && chmod a+x /app/backup
RUN mkdir /app/sqlite && chmod 1777 /app/sqlite
ENTRYPOINT ["/app/backup"]
