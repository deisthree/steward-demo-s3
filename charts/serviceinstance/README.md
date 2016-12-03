# A Steward ServiceInstance

This [Helm](https://github.com/kubernetes/helm) chart installs a new Steward `ServiceInstance` to
provision a new S3 bucket

## Installation

Installation of this chart is simple, assuming the following:

- You have the `helm` CLI and the Tiller server running (simply `helm init` to get the latter)
- Your current working directory is this folder

... install with this command:

```console
helm install .  --namespace=default --set ServiceClassNamespace="steward"
```
