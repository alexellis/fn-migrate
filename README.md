# fn-migrate

Migrate OpenFaaS functions from one cluster to another

This tool may be used until the end of April by licensed OpenFaaS Pro customers only.

## Installation

Download the correct binary for your system from the [Releases Page](https://github.com/alexellis/fn-migrate/releases)

## Pre-reqs

* The source cluster must be running the latest OpenFaaS Pro version, if not, fields will be skipped and missing. The easiest way to do this is to update the Helm chart and run an install over the top, alternatively, edit the "image" tag using `kubectl edit -n openfaas deploy/gateway` and update the faas-netes image as per: [ghcr.io/openfaasltd/faas-netes](https://github.com/openfaasltd/faas-netes/pkgs/container/faas-netes)
* The target cluster must be running in the Operator Mode - set `operator.create` to true in the Helm Chart

Ensure that any secrets referenced by functions in the source cluster are already created in the target cluster.

## Usage

Create a basic authentication URL for both the source and target cluster:

```
./fn-migrate \
  --source https://admin:xyz@cluster1.example.com \
  --target https://admin:zyx@cluster2.example.com
```

View the output:

```
fn-migrate. Copyright OpenFaaS Ltd.

Source:
 - kubernetes/faas-netes
 - version: 0.2.6
 - commit: df9c54ce65b8cfca42de3f4bc1e1ebfaf223c41d
 
 Target:
 - kubernetes/openfaas-operator
 - version: 0.2.5
 - commit: bec376f8e659912ac2b96686bcc8728e8510f938
 
 
=> Deploy: cat-key to target cluster
<= cat-key: 202 [PUT]
=> Deploy: env to target cluster
<= env: 202 [PUT]
```

Any existing functions will be updated.


