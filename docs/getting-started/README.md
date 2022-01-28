# Getting Started with Knative

Knative is an open source project that adds components for deploying, running, and managing serverless, cloud-native applications to Kubernetes. Knative eliminates the tasks of provisioning and managing servers. This lets developers focus on their code without having to worry about setting up complex infrastructure.

## Before you begin
> This Getting started guide provides instructions on how to install a local distribution of Knative for development use. The Knative Quickstart Environments shown in this guide are for experimentation use only. For production installation, see our [Installing Guide](../install/README.md)

Before you can get started with a Knative Quickstart deployment you must have the following pre-requisites: 
- Docker
- kind or minikube
- Kubernetes CLI
- Knative CLI.

Let's check if you have Docker installed ...

```bash
---
validate: $body
---
(docker info) && echo "Docker is good to go!" || echo "Please install Docker"

```

### Prepare local Kubernetes cluster

You can use [`kind`](https://kind.sigs.k8s.io/docs/user/quick-start){target=_blank} (Kubernetes in Docker) or [`minikube`](https://minikube.sigs.k8s.io/docs/start/){target=_blank} to run a local Kubernetes cluster with Docker container nodes.

Let's check if you have kind or minikube installed ...

```bash
---
validate: $body
---
((kind get clusters >& /dev/null) || (minkube start >& /dev/null)) && echo "Kind or minikube is good to go!" || echo "Please install Kind or minikube"
```

### Install the Kubernetes CLI

The [Kubernetes CLI (`kubectl`)](https://kubernetes.io/docs/tasks/tools/install-kubectl){target=_blank}, allows you to run commands against Kubernetes clusters. You can use `kubectl` to deploy applications, inspect and manage cluster resources, and view logs.

Let's see if you have kubectl installed ... 

```bash
---
validate: $body
---
(kubectl version --client >& /dev/null) && echo "kubectl is good to go!" || echo "Please install kubectl"
```

### Install the Knative CLI

The Knative CLI (`kn`) provides a quick and easy interface for creating Knative resources, such as Knative Services and Event Sources, without the need to create or modify YAML files directly.

`kn` also simplifies completion of otherwise complex procedures such as autoscaling and traffic splitting.

--8<-- "install-kn.md"

## Install the Knative "Quickstart" environment

You can get started with a local deployment of Knative by using the Knative `quickstart` plugin.

--8<-- "quickstart-install.md"
