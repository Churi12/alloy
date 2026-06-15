FROM golang:1.26.4@sha256:87a41d2539e5671777734e91f467499ed5eafb1fb1f77221dff2744db7a51775 as build
WORKDIR /app/
COPY go.mod go.sum ./
COPY syntax/go.mod syntax/go.sum ./syntax/
RUN go mod download
COPY ./integration-tests/docker/configs/kafka/ ./
RUN CGO_ENABLED=0 go build -o main main.go
FROM alpine:3.24@sha256:a2d49ea686c2adfe3c992e47dc3b5e7fa6e6b5055609400dc2acaeb241c829f4
COPY --from=build /app/main /app/main
CMD ["/app/main"]
