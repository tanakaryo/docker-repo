# syntax=docker/dockerfile:1

FROM golang:1.20-alpine3.17 AS builder

RUN apk update && apk add --no-cache gcc musl-dev sqlite-dev

WORKDIR /app

COPY ./app/go.mod ./app/go.sum ./app/hello.go ./app/doc.go ./
COPY ./app/common ./common
COPY ./app/users ./users
COPY ./app/articles ./articles

RUN go mod download

RUN GOOS=linux go build -o ./realworld

## 2nd stage
FROM alpine:3.17

WORKDIR /app

COPY --from=builder /app/realworld .

EXPOSE 8080

CMD [ "./realworld" ]