# syntax=docker/dockerfile:1
FROM golang:1.17 as builder

WORKDIR /opt/app
COPY go.* ./
RUN go mod download

COPY . .

ARG LD_FLAGS='-linkmode external -w -extldflags "-static"'
RUN go build -ldflags "$LD_FLAGS" -o example

FROM alpine as runner
WORKDIR /opt/app
COPY --from=builder /opt/app/example /opt/app/example

EXPOSE 8080
CMD ["/opt/app/example"]