# Start from golang base image
FROM golang:1.20-alpine AS builder

RUN apk add --no-cache git ca-certificates

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o main .

######## Start a new stage from scratch #######
FROM alpine:latest

RUN apk add --no-cache ca-certificates

WORKDIR /app

COPY --from=builder /app/main .

ENV PORT=8080

EXPOSE 8080

CMD ["./main"]
