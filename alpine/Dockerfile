FROM gcr.io/gcpug-container/appengine-go:alpine

ARG PROTOC_VERSION=3.8.0
ARG PROTOTOOL_VERSION=1.8.0
ARG GOLANGCI_LINT_VERSION=1.17.1

RUN curl -fo protoc.zip -sSL "https://github.com/google/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip" && \
	mkdir protoc && \
    unzip -q protoc.zip -d protoc && \
    cp ./protoc/bin/protoc /usr/local/bin/ && \
    cp -rf ./protoc/include/google /usr/local/include/ && \
    rm protoc.zip protoc -rf && \
    go get -u github.com/golang/protobuf/protoc-gen-go && \
    go get -u github.com/nametake/protoc-gen-gohttp && \
    go get -u github.com/favadi/protoc-go-inject-tag && \
    go get -u honnef.co/go/tools/cmd/staticcheck && \
    go get -u golang.org/x/lint/golint && \
    go get -u golang.org/x/tools/cmd/goimports && \
    go get -u mvdan.cc/sh/cmd/shfmt && \
    go get -u github.com/sachaos/xerrchk/cmd/xerrchk && \
    go get -u github.com/daisuzu/gsc && \
    curl -sSL https://github.com/uber/prototool/releases/download/v${PROTOTOOL_VERSION}/prototool-$(uname -s)-$(uname -m)  -o /usr/local/bin/prototool && chmod +x /usr/local/bin/prototool && \
    curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s -- -b $(go env GOPATH)/bin v${GOLANGCI_LINT_VERSION} && \
    apk add --no-cache \
        ca-certificates \
        wget \
        nodejs-npm \
        bind-tools && \
    apk del libc6-compat && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk && \
    apk add glibc-2.29-r0.apk && \
    ln -s /lib/libc.musl-x86_64.so.1 /usr/lib/libc.musl-x86_64.so.1 && \
    rm -f glibc-2.29-r0.apk && \
    rm -rf ${GOPATH}/src ${GOPATH}/pkg && \
    mkdir -p ${GOPATH}/src/github.com/googleapis && cd ${GOPATH}/src/github.com/googleapis && git clone --depth 1 https://github.com/googleapis/googleapis.git

ENV GO111MODULE on
