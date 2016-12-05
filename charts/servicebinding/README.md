# A Steward ServiceBinding

This [Helm](https://github.com/kubernetes/helm) chart installs a new Steward `ServiceBinding` to
obtain S3 bucket credentials

## Installation

Installation of this chart is simple, assuming the following:

- You have the `helm` CLI and the Tiller server running (simply `helm init` to get the latter)
- Your current working directory is this folder

... install with this command:

```console
helm install .  --namespace=default
```
