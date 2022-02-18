---
title: Install the kn CLI
codeblocks:
    - match: ^(kn version >& /dev/null) && echo "You have the Knative CLI" \|\| echo "Please install the Knative CLI"$
      validate: $body
---

### The Knative CLI (`kn`) 

```bash
(kn version >& /dev/null) && echo "You have the Knative CLI" || echo "Please install the Knative CLI"
```

--8<-- "install-kn.md"