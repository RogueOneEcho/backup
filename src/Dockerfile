FROM alpine
RUN echo "https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN apk update
RUN apk add --no-cache bash rsync sqlite b2-tools restic
WORKDIR /app
COPY logging /app/logging
COPY backup /app/backup
RUN chmod a+x /app/logging && chmod a+x /app/backup
ENTRYPOINT ["/app/backup"]
