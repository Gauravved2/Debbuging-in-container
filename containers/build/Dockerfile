FROM golang:1.17 AS builder

WORKDIR /project
COPY . .

RUN go build -o /project/bin/app

FROM ubuntu:22.04

COPY --from=builder /project/bin/app .

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    golang \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN GOINSECURE=true go install github.com/go-delve/delve/cmd/dlv@latest

ENV PATH="/root/go/bin:${PATH}"

CMD ["./app"]
