FROM golang:1.18-alpine as build
WORKDIR /app
COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go

FROM scratch
WORKDIR /app
COPY --from=build /app/main /app/main
EXPOSE 8080
CMD ["/app/main"]