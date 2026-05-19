# Contributing to Kubernetes (Fork)

Thank you for your interest in contributing to this Kubernetes fork! This document provides guidelines and information for contributors.

## Code of Conduct

This project follows the [Kubernetes Code of Conduct](https://github.com/kubernetes/community/blob/master/code-of-conduct.md). By participating, you are expected to uphold this code.

## Getting Started

### Prerequisites

- Go 1.21 or later
- Docker (for building container images)
- `make` utility
- `kubectl` for testing

### Setting Up Your Development Environment

1. Fork and clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/kubernetes.git
   cd kubernetes
   ```

2. Add the upstream remote:
   ```bash
   git remote add upstream https://github.com/kubernetes/kubernetes.git
   ```

3. Build the project:
   ```bash
   make all
   ```

4. Run tests:
   ```bash
   make test
   ```

## How to Contribute

### Reporting Bugs

Before filing a bug report, please check the [existing issues](../../issues) to avoid duplicates. Use the **Bug Report** issue template and provide:

- A clear and descriptive title
- Steps to reproduce the issue
- Expected vs. actual behavior
- Kubernetes version and environment details
- Relevant logs or error messages

### Suggesting Enhancements

Use the **Enhancement** issue template. Describe:

- The problem you're trying to solve
- Your proposed solution
- Any alternatives you've considered

### Submitting Pull Requests

1. Create a new branch from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes following the [coding conventions](#coding-conventions).

3. Write or update tests as appropriate.

4. Run the full test suite:
   ```bash
   make test
   make verify
   ```

5. Commit your changes using [Conventional Commits](https://www.conventionalcommits.org/):
   ```bash
   git commit -m "feat: add support for new scheduler plugin"
   ```

6. Push your branch and open a Pull Request.

> **Personal note:** Before pushing, I also like to run a quick focused e2e smoke test against a local kind cluster:
> ```bash
> kind create cluster --name k8s-dev
> make test-e2e FOCUS="\[Conformance\]" KUBECONFIG=~/.kube/config
> kind delete cluster --name k8s-dev
> ```
> This catches integration-level issues that unit tests alone sometimes miss.

## Coding Conventions

- Follow the [Kubernetes coding conventions](https://github.com/kubernetes/community/blob/master/contributors/guide/coding-conventions.md)
- Run `gofmt` and `golint` before submitting
- Ensure all public functions and types have godoc comments
- Keep functions small and focused
- Write unit tests for new functionality

## Syncing with Upstream

To keep your fork up to date with the upstream Kubernetes repository:

```bash
git fetch upstream
git checkout main
git merge upstream/main
```

> **Personal note:** I try to sync with upstream at least once a week to avoid large, painful merge conflicts. Running `make verify` after merging is a good habit — it catches any generated file drift (e.g. from `hack/update-codegen.sh`) before you start new work on top of the merge.
