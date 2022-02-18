### [kind](https://kind.sigs.k8s.io/docs/user/quick-start){target=_blank} (Kubernetes in Docker)
Enables you to run a local Kubernetes cluster with Docker container nodes.

```bash
---
validate: $body
---
(kind version >& /dev/null) && echo "You have Kind!" || (echo "Please install Kind" && exit 1)
```