FROM golang:1.23.4-alpine

WORKDIR /app

COPY . .

RUN go build -o server server.go

EXPOSE 8000

CMD ["./server"]