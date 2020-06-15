# sample-controller

This repository implements a simple controller for watching Foo resources as
defined with a CustomResourceDefinition (CRD).

This particular example demonstrates how to perform basic operations such as:

* How to register a new custom resource (custom resource type) of type `Foo` using a CustomResourceDefinition.
* How to create/get/list instances of your new resource type `Foo`.
* How to setup a controller on resource handling create/update/delete events.

It makes use of the generators in [k8s.io/code-generator](https://github.com/kubernetes/code-generator)
to generate a typed client, informers, listers and deep-copy functions. You can
do this yourself using the `./hack/update-codegen.sh` script.

The `update-codegen` script generate the following files & directories:

* `pkg/apis/samplecontroller/v1alpha1/zz_generated.deepcopy.go`
* `pkg/generated/`

Changes should not be made to these files manually, and when creating your own
controller based off of this implementation you should not copy these files and
instead run the `update-codegen` script to generate your own.

## How to run `update-codegen`

- clone the Repo

> The script requires the code to be cloned into the `~/k8s.io` directory

```sh
mkdir ~/k8s.io

git clone git@github.com:neoseele/sample-controller.git

cd ~/k8s.io/sample-controller
```


- create and populate vendor dir

```sh
go mod vendor
chmod +x ./vendor/k8s.io/code-generator/generate-groups.sh
```

- run `update-codegen` after making code changes

```sh
./hack/update-codegen.sh
Generating deepcopy funcs
Generating clientset for samplecontroller:v1alpha1 at k8s.io/sample-controller/pkg/generated/clientset
Generating listers for samplecontroller:v1alpha1 at k8s.io/sample-controller/pkg/generated/listers
Generating informers for samplecontroller:v1alpha1 at k8s.io/sample-controller/pkg/generated/informers
```


## Where does it come from?

https://github.com/kubernetes/sample-controller
