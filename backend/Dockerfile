# Multi-stage build for testingtestingtesting Go backend
FROM golang:1.24-alpine AS builder

WORKDIR /app

# Copy go mod files
COPY go.mod go.sum ./
RUN go mod download

# Copy source code
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o testingtestingtesting-backend ./cmd/server

# Production stage
FROM alpine:latest

RUN apk --no-cache add ca-certificates
WORKDIR /root/

# Copy the binary from builder stage
COPY --from=builder /app/testingtestingtesting-backend .

# Expose port
EXPOSE 8080

# Run the application
CMD ["./testingtestingtesting-backend"]
