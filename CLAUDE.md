# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Docker-based development container setup for Go 1.24.3 development. The project builds custom Docker images based on Debian Bookworm with Go toolchain pre-installed.

## Key Commands

### Docker Image Building
- `make test.build.arm64` - Build ARM64 Docker image
- `make test.build.amd64` - Build AMD64 Docker image  
- `make test` - Build and test both ARM64 and AMD64 images
- `make test.arm64` - Build and clean up ARM64 image
- `make test.amd64` - Build and clean up AMD64 image

### Docker Image Cleanup
- `make test.rmi.arm64` - Remove ARM64 image
- `make test.rmi.amd64` - Remove AMD64 image

## Architecture

The project uses a multi-architecture Docker build system:

- **Base Image**: `ghcr.io/bearfield/debian-fish:bookworm`
- **Target Image**: `ghcr.io/bearfield/golang:test.1.24`
- **Go Version**: 1.24.3
- **Supported Architectures**: ARM64 and AMD64

The Dockerfile installs Go 1.24.3 with necessary build tools (gcc, g++, libc6-dev, pkg-config) and sets up the Go workspace at `/go` with proper environment variables.

## Container Configuration

- **GOPATH**: `/go`
- **User**: `kumano_ryo`
- **Shell**: fish (inherited from base image)
- **Working Directory**: `$GOPATH`