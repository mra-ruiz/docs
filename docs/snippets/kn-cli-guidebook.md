### The Knative CLI (`kn`)

```bash
---
validate: $body
---
(kn version >& /dev/null) && echo "You have the Knative CLI" || (echo "Please install the Knative CLI" && exit 1)
```

### Install the Knative CLI

--8<-- "install-kn.md"