### [minikube](https://minikube.sigs.k8s.io/docs/start/){target=_blank} (Kubernetes in Docker)
Enables you to run a local Kubernetes cluster with Docker container nodes.

```bash
---
validate: $body
---
(minikube version >& /dev/null) && echo "You have minikube!" || (echo "Please install minikube" && exit 1)
```