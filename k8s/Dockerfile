FROM golang
WORKDIR /k8s-example
COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /bin/k8s-example .

FROM alpine:latest
RUN addgroup -S k8s-example && adduser -S k8s-example -G k8s-example
USER k8s-example
WORKDIR /home/k8s-example
COPY --from=build-go /bin/k8s-example ./
EXPOSE 3000
ENTRYPOINT ["./k8s-example"]
