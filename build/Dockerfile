FROM golang:1.25.5-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -o /app/telegram-nats-bridge .

FROM gcr.io/distroless/static-debian12:nonroot

COPY --from=builder /app/telegram-nats-bridge /telegram-nats-bridge

CMD ["/telegram-nats-bridge", "run", "--config", "/config/config.yaml"]