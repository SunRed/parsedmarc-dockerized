FROM alpine:latest

ADD start.sh /start.sh

RUN apk add --no-cache curl jq bash \
    && chmod +x /start.sh

ENTRYPOINT [ "/start.sh" ]
