FROM golang:1.27.4-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea as build

ARG GOFLAGS=""
ENV GOFLAGS=$GOFLAGS

WORKDIR /build

COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .

RUN go build ./trillian/ctfe/ct_server

FROM gcr.io/distroless/base-debian12@sha256:d605e138bb398428779e5ab490a6bbeeabfd2551bd919578b1044718e5c30798

COPY --from=build /build/ct_server /

ENTRYPOINT ["/ct_server"]
