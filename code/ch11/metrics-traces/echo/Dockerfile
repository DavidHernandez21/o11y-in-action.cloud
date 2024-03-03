FROM golang:1.22.0-bookworm AS builder
WORKDIR /build
COPY go.mod .
COPY . .
RUN go get -u ./... && go mod tidy && go mod vendor && \
    GOPROXY=off go build -o echo -mod=vendor main.go

FROM debian:bookworm-slim
WORKDIR /app
COPY --from=builder /build/echo /app/echo
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
CMD ["./echo"]
