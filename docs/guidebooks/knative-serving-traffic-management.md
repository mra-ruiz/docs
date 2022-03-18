---
title: Knative Serving - Traffic Management
layout:
    1: left
    2: right
    default: wizard
imports:
    - docs/snippets/docker-guidebook.md
    - docs/install/README.md
    - docs/snippets/install-kn.md
    - docs/snippets/kubectl-guidebook.md
wizard:
    steps:
        - Using tags to create target URLs
        - Traffic routing examples
        - Routing and managing traffic by using the Knative CLI
        - Routing and managing traffic with blue/green deployment
        # - Clean Up
codeblocks:
    # Validation for Step 3: Routing and managing traffic by using the Knative CLI
    - match: ^kn service update <service-name> --traffic <revision-name>=<percent>$
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kn service update example-service --traffic green=80 --traffic blue=20$
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kn service update example --tag green=revision-0001 --tag blue=@latest$
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kn service update example-service --traffic @latest=80 --traffic v1=20$
      validate: $? -e 0 && exit 0 \|\| exit 1
    # Validation for Step 4: Routing and managing traffic with blue/green deployment
    - match: ^kubectl get configurations <service-name> -o=jsonpath='{.status.latestCreatedRevisionName}'$
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kubectl get route <route-name>$
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kubectl get configurations <service-name> -o=jsonpath='{.status.latestCreatedRevisionName}'$
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kubectl get route <route-name> --output jsonpath="{.status.traffic[*].url}"$
      validate: $? -e 0 && exit 0 \|\| exit 1
---

--8<-- "https://raw.githubusercontent.com/kubernetes-sigs/kui/master/plugins/plugin-kubectl/notebooks/knative-what-is-it-good-for.md"

---

::imports

---

--8<-- "docs/serving/traffic-management.md"

<!-- --8<-- "../docs/getting-started/clean-up.md" -->