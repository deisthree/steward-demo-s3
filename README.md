# Steward S3 Demo

This repository contains helm charts intended to demo
[Steward CF](https://github.com/deis/steward-cf).


The following charts are available:

# charts/s3-service-provider

This chart installs the following:

* A configured s3-cf-broker (the broker is taken from a [CloudFoundry community implementation](https://github.com/cloudfoundry-community/s3-broker)
* A Steward CF instance

## Broker Details

When an `Instance` is later created, steward-cf will call the backing CF service
broker's provision API to create a new S3 bucket. When a `Binding` is created,
steward-cf will call the backing CF service broker's binding API to create
an IAM user and grant access to the aforementioned bucket.

## Steward Details

After a bind, steward-cf will drop the bucket-name, `AWS_ACCESS_KEY`, and
`AWS_SECRET_KEY` into a kubernetes Secret. It will look like the following:

```yaml
kind: Secret
apiVersion: v1
data:
  name: <s3 bucket name>
  password: <AWS_SECRET_KEY>
  username: <AWS_ACCESS_KEY>
```

# charts/broker

This chart installs a `Broker` resource, which tells `steward-cf` to connect to
the backing S3 CF service broker API, list its catalog, and write a
`ServiceClass` resource for each service therein

# charts/instance

This chart installs an `Instance` resource, which tells `steward-cf` to make a
provision API call on the backing S3 CF broker API. This call in turn creates
a new S3 bucket.

# charts/binding

This chart installs a `Binding` resource, which tells `steward-cf` to make a
bind API call on the backing S3 CF broker API. This call in turn creates new IAM
credentials which get written into a secret called `s3-demo-secret`, in the same
namespace as the `Binding` itself.

# charts/s3-uploader

This chart installs a job that consumes the secret output from the charts/binding
chart, connects to the S3 bucket described in the secret, and uploads a jpeg
image to the bucket.


# Prerequisites

You must have AWS credentials with full S3 and IAM access. The access key
should be stored in the `AWS_ACCESS_KEY_ID` environment variable, and the secret
 should be stored in the `AWS_SECRET_ACCESS_KEY` environment variable.

# Demo

In order to use these helm charts to show a start-to-finish demo of Steward's capability, install the following charts in order:

1. [s3-service-provider](./charts/s3-service-provider) to install the backing CF service broker
1. [steward-cf](.charts/steward-cf) to install steward-cf
1. [servicebroker](./charts/servicebroker) to install the `ServiceBroker` resource
  - After this step, a list of `ServiceClass` resources should be written to
  the `steward` namespace
1. [serviceinstance](./charts/serviceinstance) to install the `ServiceInstance` resource
  - After this step, an S3 bucket should be provisioned in response to the creation of that
  resource
1. [servicebinding](./charts/servicebinding) to install the `ServiceBinding` resource
  - After this step, a secret called `s3-demo-secret` should be written to the
  same namespace as the `ServiceBinding` resource itself
1. [s3-uploader](./charts/s3-uploader) to run the uploader job
