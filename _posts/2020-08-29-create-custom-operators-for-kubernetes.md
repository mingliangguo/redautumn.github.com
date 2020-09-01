---
title: "Create custom operators for kubernetes"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-08-29 12:22:33 EDT
---

## Create custom resources for kubernetes

## How to extend kubernetes

### Extension patterns

> There is a specific pattern for writing client programs that work well with Kubernetes called the Controller pattern. Controllers typically read an object's .spec, possibly do things, and then update the object's .status.
> A controller is a client of Kubernetes. When Kubernetes is the client and calls out to a remote service, it is called a Webhook. The remote service is called a Webhook Backend. Like Controllers, Webhooks do add a point of failure.

### The controller pattern

> The Controller Pattern
Whether you use CRDs or an aggregated API, the best way to implement the behavior of your custom resources is using the controller pattern, the same way Kubernetes controls its own resources. It is often described by three adjectives: declarative, asynchronous and level-based; most of its mechanics are implemented in Go in client-go/tools/cache and client-go/util/workqueue and documented in several blogs.

> 1. The user declares the desired state of an object, e.g. kubectl apply -f mapping.yaml, where mapping.yaml contains the specification (Spec) of a Mapping object. The Kubernetes API responds as soon as the desired state has been stored in etcd, but before the user’s intent has been fulfilled—which is to create a dummy Service object, owned by the Mapping object, annotated according to its Spec.
> 2. Asynchronously, the controller watches for CRUD events on the Mapping and Service resources. For each event, the state of the corresponding object is cached, and its key goes to a work queue; the key is the namespace and name of the Mapping object, obtained directly, or via owner references for Service events. This logic is the work of listers and informers.
> 3. The work queue is backed by a queue and a set, so that if a key is added multiple times before it is processed, it is only processed once. The processing function gets the latest state of the Mapping and Service objects from cache, updates the Mapping’s Status (e.g. Service not yet created, or outdated annotation) and takes action to reconcile it according to the Spec (e.g. create the dummy Service, or update its annotation; other use cases could place calls to external services here). Thus, the control loop is level-based, because it reconciles the desired and observed states based on their latest observations, not on their historical changes.

## Kubebuilder v.s. operator sdk


Refer to: https://github.com/operator-framework/operator-sdk/issues/1758#issuecomment-517432349

> There's not a huge difference between the Go projects that kubebuilder and operator-sdk scaffold. Both use controller-tools and controller-runtime and both scaffold substantially similar go package structures.

> Where they differ is:
>
> - Operator SDK also has support for Ansible and Helm operators, which make it easy to write operators without having to learn Go and if you already have experience with Ansible or Helm
> - Operator SDK includes integrations with the Operator Lifecycle Manager (OLM), which is a key component of the Operator Framework that is important to Day 2 cluster operations, like managing a live upgrade of your operator.
> - Operator SDK includes a scorecard subcommand that helps you understand if your operator follows best practices.
> - Operator SDK includes an e2e testing framework that simplifies testing your operator against an actual cluster.
> - Kubebuilder includes an envtest package that allows operator developers to run simple tests with a standalone etcd and apiserver.
> - Kubebuilder scaffolds a Makefile to assist users in operator tasks (build, test, run, code generation, etc.); Operator SDK is currently using built-in subcommands. Each has pros and cons. The SDK team will likely be migrating to a Makefile-based approach in the future.
> - Kubebuilder uses Kustomize to build deployment manifests; Operator SDK uses static files with placeholders.
> - Kubebuilder has recently improved its support for admission and CRD conversion webhooks, which has not yet made it into SDK.
> The SDK and Kubebuilder teams work closely together, and we're planning to increase our efforts to help the kubebuilder team maintain controller-tools and controller-runtime so that the entire community has access to the latest features and bug fixes.

## References

- [Extending your Kubernetes Cluster](https://kubernetes.io/docs/concepts/extend-kubernetes/extend-cluster/)
- [Kubernetes Custom Resource, Controller and Operator Development Tools](https://admiralty.io/blog/kubernetes-custom-resource-controller-and-operator-development-tools/)
- Refer to [Azure Databriks operator](https://github.com/microsoft/azure-databricks-operator) for a real project implemented using `kubebuilder`
