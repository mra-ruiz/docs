### [Docker](https://docs.docker.com/get-docker/)

```bash
---
validate: $body
---
(docker info >& /dev/null) && echo “You have Docker!” || (echo “Please install Docker” && exit 1)
```