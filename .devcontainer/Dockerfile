FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# Install system packages and Docker Compose plugin
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        curl \
        wget \
        ca-certificates \
        docker-compose-v2 \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install Go 1.23
RUN wget -q https://go.dev/dl/go1.23.0.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.23.0.linux-amd64.tar.gz \
    && rm go1.23.0.linux-amd64.tar.gz

ENV PATH="/usr/local/go/bin:${PATH}"
ENV GOPATH="/go"
ENV PATH="${GOPATH}/bin:${PATH}"

# Install Temporal CLI
RUN curl -sSf https://temporal.download/cli.sh | sh \
    && mv /root/.temporalio/bin/temporal /usr/local/bin/temporal

# Install Go development tools
RUN go install honnef.co/go/tools/cmd/staticcheck@latest \
    && go install github.com/kisielk/errcheck@latest \
    && go install go.temporal.io/sdk/contrib/tools/workflowcheck@latest
