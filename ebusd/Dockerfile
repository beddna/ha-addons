ARG BUILD_FROM
FROM $BUILD_FROM

ENV LANG C.UTF-8

# Aktualizuj repo
RUN apk update

# Přidej edge repo
RUN echo "https://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN echo "https://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories
RUN apk update

# Nejnovější ebusd (26.1+)
RUN apk add --no-cache ebusd

LABEL Description="ebusd 26.1+"

COPY run.sh /
RUN chmod a+x /run.sh
CMD [ "/run.sh" ]

# Health check
HEALTHCHECK --interval=5m --timeout=3s --start-period=90s \
   CMD nc -z 127.0.0.1 8888 || exit 1

