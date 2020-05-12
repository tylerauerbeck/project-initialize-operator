Project Initialize Operator
========================================

_This repository is currently undergoing active development. Functionality may be in flux_

## Overview

This repository contains the project initialize operator which provides functionality for creating new projects within OpenShift and triggering custom onboarding processes, specifically around the GitOps solution [ArgoCD](https://argoproj.github.io/argo-cd/).


### Install (OpenShift)

Run the following steps to run the operator locally. The operator will require `cluster-admin` permissions that can be applied using the resources provided in the deploy/ folder.

Prerequisites:

In order to run the operator locally, you will need to meet these [prerequisites](https://github.com/operator-framework/operator-sdk#prerequisites) and then follow these [instructions](https://github.com/operator-framework/operator-sdk/blob/master/doc/user/install-operator-sdk.md#install-the-operator-sdk-cli) to install the operator-sdk.

Create the expected namespace
```
$ oc new-project project-operator
```

Add projectinitialize crd and resources to cluster
```
$ oc apply -f deploy/service_account.yaml
$ oc apply -f deploy/role.yaml
$ oc apply -f deploy/role_binding.yaml
```

### Add ProjectInitialize CRD
#### 4.X OCP
```
$ oc apply -f deploy/crds/redhatcop.redhat.io_projectinitializes_crd.yaml
```
#### 3.X OCP
```
$ oc apply -f deploy/crds/redhatcop.redhat.io_projectinitializes_crd_3x.yaml
```

### Add ProjectInitialize CRD
#### 4.X OCP
```
$ oc apply -f deploy/crds/redhatcop.redhat.io_projectinitializequota_crd.yaml
```
#### 3.X OCP
```
$ oc apply -f deploy/crds/redhatcop.redhat.io_projectinitializequota_crd_3x.yaml
```
### Deploy Operator (OpenShift)
Run the following command when ready to deploy the operator into cluster it will monitor

<<<<<<< HEAD
### Run Locally (OpenShift)
`This should only be for development purposes`
Pull in dependences
```
$ export GO111MODULE=on
$ go mod vendor
```

Login to the cluster via the Service Account shown in the above install step
=======
>>>>>>> 2574d60a91b9d4b256a3e87e3de586977ffffd2f
```
$ oc apply -f deploy/operator.yaml
```

<<<<<<< HEAD
Run Operator-SDK locally
```
$ operator-sdk run --local --namespace="project-operator" 
```

### Deploy Operator (OpenShift)
Run the following command when ready to deploy the operator into cluster it will monitor

```
$ oc apply -f deploy/operator.yaml
```
=======
### Adding Defined Quota Sizes to Cluster

When the `quotaSize` attribute is defined in the `ProjectInitializeQuota` Custom Resource (CR) the operator will search for a cluster level `ProjectInitializeQuota` CR that defines a praticular quota size. This can be used to define predetermined t-shirt sizes when creating new projects (small, medium, large, etc)

```
apiVersion: redhatcop.redhat.io/v1alpha1
kind: ProjectInitializeQuota
metadata:
  name: small
spec:
  hard:
    cpu: "5"
    memory: "10Gi"
    pods: "10"
```


## Example Workflow
The project initialize operator will need to be running in the project-operator namespace before running the following example workslow.


### Apply T-Shirt Size
First start by applying the `ProjectInitializeQuota` CR that will be a global t-shirt size placeholder that the  initializer can reference when applying quotas to new projects.
```
$ oc apply -f deploy/examples/small_projectqouta_cr.yaml
```

### Apply Project Initializer
Apply the `ProjectInitialize` CR which contains details about the dev team name, cluster name, and a reference to the `ProjectInitializeQuota` which will specify the quota to assign the namespace. 
```
$ oc apply -f deploy/examples/basic_projectinit_cr.yaml
```

## Development
### [How-To](docs/development.md)
>>>>>>> 2574d60a91b9d4b256a3e87e3de586977ffffd2f
