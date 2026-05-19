# Kubernetes Fork

This repository is a fork of [kubernetes/kubernetes](https://github.com/kubernetes/kubernetes), the open-source container orchestration system.

## Overview

Kubernetes (K8s) is an open-source system for automating deployment, scaling, and management of containerized applications. It groups containers that make up an application into logical units for easy management and discovery.

## Prerequisites

- Go 1.21+
- Docker 20.10+
- `make`
- `git`

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/your-org/kubernetes.git
cd kubernetes
```

### Build

Build all components:

```bash
make all
```

Build a specific component (e.g., `kubectl`):

```bash
make WHAT=cmd/kubectl
```

### Run Tests

Run unit tests:

```bash
make test
```

Run integration tests:

```bash
make test-integration
```

Run end-to-end tests:

```bash
make test-e2e
```

## Development

### Code Generation

Some files in this repository are generated. To regenerate them:

```bash
make generate
```

See [`.generated_files`](.generated_files) for a list of generated files.

### Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting pull requests.

## Differences from Upstream

This fork tracks upstream `kubernetes/kubernetes`. Notable local changes:

- *(Document any divergences from upstream here)*

## Syncing with Upstream

To pull in the latest changes from the upstream repository:

```bash
git remote add upstream https://github.com/kubernetes/kubernetes.git
git fetch upstream
git merge upstream/main
```

> **Note:** The upstream default branch was renamed from `master` to `main`. Updated the merge command accordingly.

> **Personal note:** I prefer rebasing over merging to keep a cleaner local history. Use `git rebase upstream/main` instead if you want a linear commit log.

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
