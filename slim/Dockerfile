FROM gcr.io/gcpug-container/appengine-go:slim

ARG GOLANGCI_LINT_VERSION=v1.23.1

RUN cd $(mktemp -d); go mod init tmp; go get -u github.com/99designs/gqlgen; cd - && \
    cd $(mktemp -d); go mod init tmp; go get -u golang.org/x/tools/cmd/goimports; cd - && \
    cd $(mktemp -d); go mod init tmp; go get mvdan.cc/gofumpt/gofumports; cd - && \
    cd $(mktemp -d); go mod init tmp; go get mvdan.cc/sh/v3/cmd/shfmt; cd - && \
    curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s -- -b $(go env GOPATH)/bin v${GOLANGCI_LINT_VERSION} && \
    go get -u github.com/sachaos/xerrchk/cmd/xerrchk && \
    cd $(mktemp -d); go mod init tmp; go get -u github.com/daisuzu/gsc; cd - && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    \
    apt-get update && \
	apt-get install -yqq --no-install-suggests --no-install-recommends \
		npm \
		dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf ${GOPATH}/src ${GOPATH}/pkg && \
    mkdir -p ${GOPATH}/src/github.com/googleapis && cd ${GOPATH}/src/github.com/googleapis && git clone --depth 1 https://github.com/googleapis/googleapis.git

ENV GO111MODULE on

