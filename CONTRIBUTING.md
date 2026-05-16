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

> **Personal note:** I try to sync with upstream at least once a week to avoid large, painful merge conflicts. Running `make verify` after syncing is a good habit to catch any breaking changes early. I also run `make test WHAT=./pkg/scheduler/...` after syncing since that's the area I'm most actively experimenting with.
>
> **Tip:** If `make verify` fails after a sync due to generated file drift, running `make update` first usually fixes it before re-running `make verify`.

## Review Process

- All PRs require at least one approval from a maintainer listed in [OWNERS](.github/OWNERS)
- CI checks must pass before merging
- Large changes should be broken into smaller, focused PRs when possible
