ARG ALPINE_VERSION=3.22.4
FROM alpine:${ALPINE_VERSION}
RUN apk add --no-cache bash rsync sqlite restic
WORKDIR /app
COPY logging /app/logging
COPY backup /app/backup
RUN chmod a+x /app/logging && chmod a+x /app/backup
ENTRYPOINT ["/app/backup"]
