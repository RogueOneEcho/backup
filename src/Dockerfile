ARG ALPINE_VERSION=3.24.2
FROM alpine:${ALPINE_VERSION}
RUN apk add --no-cache bash sqlite restic
WORKDIR /app
COPY logging /app/logging
COPY backup /app/backup
RUN chmod a+x /app/logging && chmod a+x /app/backup
RUN mkdir /app/sqlite && chmod 1777 /app/sqlite
ENTRYPOINT ["/app/backup"]
