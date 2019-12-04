FROM gcr.io/gcpug-container/appengine-go:slim

ARG PROTOC_VERSION=3.10.0
ARG PROTOTOOL_VERSION=1.9.0
ARG GOLANGCI_LINT_VERSION=1.21.0

RUN curl -fo protoc.zip -sSL "https://github.com/google/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip" && \
	mkdir protoc && \
    unzip -q protoc.zip -d protoc && \
    cp ./protoc/bin/protoc /usr/local/bin/ && \
    cp -rf ./protoc/include/google /usr/local/include/ && \
    rm protoc.zip protoc -rf && \
    go get -u github.com/sachaos/xerrchk/cmd/xerrchk && \
    cd $(mktemp -d); go mod init tmp;go get -u github.com/99designs/gqlgen && \
    go get -u github.com/golang/protobuf/protoc-gen-go && \
    go get -u github.com/nametake/protoc-gen-gohttp && \
    go get -u github.com/favadi/protoc-go-inject-tag && \
    curl -sSL https://github.com/uber/prototool/releases/download/v${PROTOTOOL_VERSION}/prototool-$(uname -s)-$(uname -m)  -o /usr/local/bin/prototool && chmod +x /usr/local/bin/prototool && \
    go get -u github.com/sonatard/pblint && \
    go get -u golang.org/x/tools/cmd/goimports && \
    cd $(mktemp -d); go mod init tmp; go get mvdan.cc/gofumpt/gofumports && \
    go get -u mvdan.cc/sh/cmd/shfmt && \
    go get -u golang.org/x/lint/golint && \
    curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s -- -b $(go env GOPATH)/bin v${GOLANGCI_LINT_VERSION} && \
    go get -u honnef.co/go/tools/cmd/staticcheck && \
    go get -u mvdan.cc/unparam && \
    go get -u gitlab.com/opennota/check/cmd/structcheck && \
    go get -u gitlab.com/opennota/check/cmd/varcheck && \
    go get -u github.com/daisuzu/gsc && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    \
 	apt-get update && \
	apt-get install -yqq --no-install-suggests --no-install-recommends \
		npm \
		dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf ${GOPATH}/src ${GOPATH}/pkg && \
    mkdir -p ${GOPATH}/src/github.com/googleapis && cd ${GOPATH}/src/github.com/googleapis && git clone --depth 1 https://github.com/googleapis/googleapis.git

RUN go get -u github.com/envoyproxy/protoc-gen-validate && cd $GOPATH/src/github.com/envoyproxy/protoc-gen-validate && make build 

ENV GO111MODULE on

