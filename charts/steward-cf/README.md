# Steward CF

This [Helm](https://github.com/kubernetes/helm) chart installs [Steward CF](https://github.com/deis/steward-cf).

## Installation

Installation is simple. Assuming the following:

- You have the `helm` CLI and the Tiller server running (simply `helm init` to get the latter)
- Your current working directory is this folder

... install with this command:

```console
helm install . --namespace steward
```
