FROM gcr.io/gcpug-container/appengine-go:alpine

ARG PROTOC_VERSION=3.6.1
ARG PROTOTOOL_VERSION=1.3.0
ARG GOLANGCI_LINT_VERSION 1.12.5
ENV GO111MODULE on

RUN	curl -fo protoc.zip -sSL "https://github.com/google/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip" && \
	mkdir protoc && \
    unzip -q protoc.zip -d protoc && \
    cp ./protoc/bin/protoc /usr/local/bin/ && \
    cp -rf ./protoc/include/google /usr/local/include/ && \
    rm protoc.zip protoc -rf && \
    go mod init tmp && \
    go get -u github.com/golang/protobuf/protoc-gen-go@v1.2.0 && \
    go get -u github.com/nametake/protoc-gen-gohttp && \
    go get -u github.com/favadi/protoc-go-inject-tag && \
    go get -u honnef.co/go/tools/cmd/staticcheck && \
    go get -u golang.org/x/lint/golint && \
    go get -u golang.org/x/tools/cmd/goimports && \
    go get -u mvdan.cc/sh/cmd/shfmt && \
    rm -rf ${GOPATH}/src/github.com/golang ${GOPATH}/pkg && \
    curl -sSL https://github.com/uber/prototool/releases/download/v${PROTOTOOL_VERSION}/prototool-$(uname -s)-$(uname -m)  -o /usr/local/bin/prototool && chmod +x /usr/local/bin/prototool && \
    curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s -- -b $(go env GOPATH)/bin v${GOLANGCI_LINT_VERSION} && \
    apk add --no-cache \
        nodejs-npm \
        bind-tools

