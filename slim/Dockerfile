FROM gcr.io/gcpug-container/appengine-go:slim

RUN cd $(mktemp -d); go mod init tmp; go get -u github.com/99designs/gqlgen; cd - && \
    cd $(mktemp -d); go mod init tmp; go get -u golang.org/x/tools/cmd/goimports; cd - && \
    cd $(mktemp -d); go mod init tmp; go get mvdan.cc/gofumpt/gofumports; cd - && \
    cd $(mktemp -d); go mod init tmp; go get mvdan.cc/sh/v3/cmd/shfmt; cd - && \
    cd $(mktemp -d); go mod init tmp; go get -u github.com/daisuzu/gsc; cd - && \
    cd $(mktemp -d); git clone https://github.com/Yamashou/gqlgenc.git; cd gqlgenc; go build .; mv gqlgenc $GOPATH/bin && \
    go get -u github.com/sachaos/xerrchk/cmd/xerrchk && \
    GOLANGCI_LINT_LATEST_VERSION=$(basename $(curl -s -o /dev/null -w '%{redirect_url}'  https://github.com/golangci/golangci-lint/releases/latest)) && \
    curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin ${GOLANGCI_LINT_LATEST_VERSION} && \
    \
    apt-get update && \
	apt-get install -yqq --no-install-suggests --no-install-recommends \
		npm \
		dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf ${GOPATH}/src ${GOPATH}/pkg
