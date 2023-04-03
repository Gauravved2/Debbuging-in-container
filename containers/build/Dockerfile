FROM golang:1.17 AS builder
RUN go get github.com/go-delve/delve/cmd/dlv
WORKDIR /project
COPY . .
RUN go build -o /project/bin/app
FROM ubuntu:22.04
COPY --from=builder /project/bin/app .
CMD [ "./app" ]