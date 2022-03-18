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
        - name: Using tags to create target URLs
        - name: Traffic routing examples
        - name: Routing and managing traffic by using the Knative CLI
        - name: Routing and managing traffic with blue/green deployment
codeblocks:
    # Validation for Step 1: Using tags to create target URLs
    - match: ^git clone https://github.com/knative/docs.git knative-docs
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^go mod init github.com/knative/docs/code-samples/
      validate: ls go.mod
    # Validation for Step 2: Traffic routing examples
    - match: ^# Build the container on your local machine
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^kubectl apply --filename service.yaml$
      validate: kn service describe service
    - match: ^kubectl get ksvc helloworld-go  --output=custom-columns=NAME:.metadata.name,URL:.status.url$
      validate: $body
    - match: ^ NAME
      optional: true
    - match: ^kn service create helloworld-go --image=docker.io/{username}/helloworld-go --env TARGET="Go Sample v1"$
      validate: kn service describe helloworld-go
    - match: ^Creating service 'helloworld-go' in namespace 'default'
      optional: true
    # Validation for Step 3: Routing and managing traffic by using the Knative CLI
    - match: ^curl http://hello.default.127.0.0.1.sslip.io$
      validate: $body
    # Validation for Step 4: Routing and managing traffic with blue/green deployment
    - match: ^kubectl delete --filename service.yaml$
    - match : ^kn service delete helloworld-go$
    - match: ^kind delete clusters knative$
      validate: \(kubectl cluster-info --context kind-knative\) && exit 1 \|\| exit 0
    - match: ^minikube delete -p knative$
      validate: \(kubectl cluster-info --context kind-knative\) && exit 1 \|\| exit 0
---

--8<-- "https://raw.githubusercontent.com/kubernetes-sigs/kui/master/plugins/plugin-kubectl/notebooks/knative-what-is-it-good-for.md"

---

::imports

---

--8<-- "docs/serving/traffic-management.md"

<!-- --8<-- "../docs/getting-started/clean-up.md" -->
