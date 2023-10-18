FROM golang:1.16-alpine3.15 as build-stage
WORKDIR /usr/src/app
COPY . .
ENV REQUEST_ORIGIN http://localhost:5000/
RUN go build && \
    adduser -S appuser && \
    chown appuser .

FROM alpine
EXPOSE 8080
WORKDIR /usr/src/app
COPY --from=build-stage /usr/src/app /usr/src/app
COPY --from=build-stage /etc/passwd /etc/passwd
USER appuser
CMD ["./server"]