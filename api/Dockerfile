FROM ubuntu:latest
FROM golang:alpine as builder
LABEL authors="mediablocker"

RUN mkdir /build

ADD . /build/

WORKDIR /build

RUN go build -o main .


# Install dependencies
RUN go mod download

#stage 2

FROM alpine

RUN adduser -S -D -H -h /app appuser

USER appuser

COPY . /app

COPY --from=builder /build/main /app/

# User with fewer privileges
USER appuser

WORKDIR /app

EXPOSE 3000

CMD ["./main"]
