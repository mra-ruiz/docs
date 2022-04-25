---
title: Knative Serving - Hello World
layout:
    1: left
    2: right
    default: wizard
imports:
  - docs/install/README.md
wizard:
    steps:
        - name: Install Required Tools
          description: Install Knative Serving and the kn CLI
        - match: Building
          name: Building your application
          description: In this example, you will build a "Hello world" application
        - name: Deploying
          description: After build is complete, push container to docker hub and then deploy your app into your cluster
        - match: Verifying
          name: Ping your Knative Service
        - match: Removing
          name: Clean Up
codeblocks:
    # Validation for Step 2: Building your application
    - match: ^git clone https://github.com/knative/docs.git knative-docs
      validate: $? -e 0 && exit 0 \|\| exit 1
    - match: ^go mod init github.com/knative/docs/code-samples/
      validate: ls go.mod
    # Validation for Step 3: Deploying your service
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
    # Validation for Step 4: Pinging your Knative Service
    - match: ^curl http://hello.default.127.0.0.1.sslip.io$
      validate: $body
    # Validation for Step 5: Clean Up
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

# Knative Serving - Deploying Hello World

This application will be deplyoyed as a Knative Service instead of a Kubernetes service.

---

# Install Required Tools

!!! note "Note - Installing Knative" 
    If you install Knative using Quickstart, when you run the quickstart plugin, a cluster called `knative` will be created. To complete the deployment of the "Hello World" application, a pre-built app with a container already pushed to Docker hub will be used.

--8<-- "code-samples/serving/hello-world/helloworld-go/README.md"