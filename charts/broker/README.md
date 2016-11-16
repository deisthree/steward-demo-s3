# Steward Broker

This [Helm](https://github.com/kubernetes/helm) chart installs a new `Broker`
resource that tells Steward to connect to the S3 backing CF service broker

# Installation

Installation of this chart is simple. Assuming the following:

- You have the `helm` CLI and the Tiller server running (simply `helm init` to get the latter)
- Your current working directory is this folder

... install with this command:

```console
helm install .  --namespace=steward
```
