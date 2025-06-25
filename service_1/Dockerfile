# Use the official Go image
FROM golang:1.22-alpine

WORKDIR /app
COPY . .

RUN apk add --no-cache curl \
    && go build -o service1

EXPOSE 8001

CMD ["./service1"]
