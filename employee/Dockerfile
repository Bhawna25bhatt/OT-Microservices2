FROM golang:1.18 as builder
MAINTAINER OpsTree Solutions
FROM golang:1.18 as builder
MAINTAINER OpsTree Solutions
#RUN go get -u go.opentelemetry.io/otel \
 #   && go get -u go.opentelemetry.io/otel/exporters/otlp \
  #  && go get -u go.opentelemetry.io/otel/exporters/stdout \
   # && go get -u go.opentelemetry.io/otel/sdk/trace
COPY ./ /go/src/employee
WORKDIR /go/src/employee
RUN go get -v -t -d ./... \
    && go build -o employee

FROM alpine:latest
MAINTAINER OpsTree Solutions
WORKDIR /app
RUN apk add --no-cache libc6-compat curl
COPY --from=builder /go/src/employee/employee /app/
COPY ./config.yaml /root/config/config.yaml
ENV CONFIG_FILE "/root/config/config.yaml"
EXPOSE 8083
ENTRYPOINT ["./employee"]
