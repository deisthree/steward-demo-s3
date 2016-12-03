# Steward Broker

This [Helm](https://github.com/kubernetes/helm) chart installs a new `Broker` resource that connects Steward CF to the S3 service provider

## Installation

Installation of this chart is simple. Assuming the following:

- You have the `helm` CLI and the Tiller server running (simply `helm init` to get the latter)
- Your current working directory is this folder

... install with this command:

```console
helm install .  --namespace=steward --set BrokerReleaseName="${RELEASE_NAME}"
```

... where `${RELEASE_NAME}` is the name of the release created when the
../s3-service-provider chart was installed
