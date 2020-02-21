# Contributing Guidelines

The Redash Chart project accepts contributions via GitHub pull requests. This document outlines the process to help get your contribution accepted.

### Reporting a Bug in Redash

This repository is used by Chart developers for maintaining the Redash chart for Kubernetes Helm. If your issue is in the Redash tool itself, please use the issue tracker in the [getredash/redash](https://github.com/getredash/redash) repository.

Before opening a new issue or submitting a new pull request, it's helpful to search the project - it's likely that another user has already reported the issue you're facing, or it's a known issue that we're already aware of.

## How to Contribute

1. Fork this repository, develop and test your Chart changes.
1. Ensure your Chart changes follow the [technical](#technical-requirements).
1. Submit a pull request.

### Technical Requirements

- Must pass the linter (`helm lint`)
- The [README](README.md) file must be regenerated using [helm-docs](https://github.com/norwoodj/helm-docs) - you can run this manually or use the [pre-commit hook](#pre-commit-hook)
- Must successfully launch following basic steps in the [README](README.md)
  - All pods go to the running state (or NOTES.txt provides further instructions if a required value is missing e.g. [minecraft](https://github.com/helm/charts/blob/master/stable/minecraft/templates/NOTES.txt#L3))
  - All services have at least one endpoint
- Must be up-to-date with the latest stable Helm/Kubernetes features
- Should follow Kubernetes best practices
  - Include Health Checks wherever practical
  - Allow configurable [resource requests and limits](http://kubernetes.io/docs/user-guide/compute-resources/#resource-requests-and-limits-of-pod-and-container)
- Provide a method for data persistence (if applicable)
- Support application upgrades
- Allow customization of the application configuration
- Provide a secure default configuration
- Do not leverage alpha features of Kubernetes
- Follows [best practices](https://github.com/helm/helm/tree/master/docs/chart_best_practices)
  (especially for [labels](https://github.com/helm/helm/blob/master/docs/chart_best_practices/labels.md)
  and [values](https://github.com/helm/helm/blob/master/docs/chart_best_practices/values.md))

### Pre-commit Hook Setup

- Install [helm-docs](https://github.com/norwoodj/helm-docs)
- Install [the pre-commit binary](https://pre-commit.com/#install)
- Then run:

```bash
pre-commit install
pre-commit install-hooks
```

Future changes to your charts requirements.yaml, values.yaml, or Chart.yaml files will cause an update to documentation when you commit.

### Merge Approval and Release Process

A Charts maintainer will review the Chart change submission, and the validation job in the CI to verify the technical requirements of the Chart.

Once the change request looks good it will be merged. This will trigger the publish job to automatically run in the CI to package and release the Chart to the repository.