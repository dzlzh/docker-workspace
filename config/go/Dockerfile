# Build
ARG GO_VERSION
FROM golang:${GO_VERSION}-alpine AS build
WORKDIR /go/src
ADD . .
RUN CGO_ENABLED=0 GOOS=linux GOPROXY=https://goproxy.cn,direct go build -ldflags="-s -w" -o app .

# Certs
FROM alpine AS certs
RUN apk --update add ca-certificates

# 运行
FROM scratch AS prod
ARG TZ
RUN apk add --no-cache tzdata
ENV TZ ${TZ}
COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=build /go/src/app .
CMD ["./app"]
