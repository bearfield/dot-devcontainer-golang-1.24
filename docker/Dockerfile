FROM ghcr.io/bearfield/debian-fish:bookworm
#
# Build arguments
ARG GOLANG_VERSION=1.24.3
ARG USER_NAME=devuser
#
# set env
ENV GOLANG_VERSION=${GOLANG_VERSION}
ENV PATH=/usr/local/go/bin:$PATH
#
# Install go 1.24.
USER root
SHELL ["/bin/bash", "-c"]
RUN	apt-get update \
    && apt-get install -y --no-install-recommends \
        g++ \
        gcc \
        libc6-dev \
        pkg-config \
    && rm -rf /var/lib/apt/lists/*
RUN curl -o go.tgz https://dl.google.com/go/go$GOLANG_VERSION.linux-$(dpkg --print-architecture).tar.gz \
    && tar -C /usr/local -xzf go.tgz \
    && rm go.tgz \
    && go version
ENV GOPATH=/go
ENV PATH=$GOPATH/bin:$PATH
RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH
USER $USER_NAME
# set env
ENV DEBIAN_FRONTEND=dialog
LABEL org.opencontainers.image.source="https://github.com/bearfield/dot-devcontainer-golang-1.24"