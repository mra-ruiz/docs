---
title: Install Knative - Quickstart
layout:
    1: left
    2: right
    default: wizard
imports:
    - docker-guidebook.md
    - kind-guidebook.md
    - minikube-guidebook.md
    - kubectl-guidebook.md
    - kn-cli-guidebook.md
wizard:
    steps:
        - match: Install Knative using quickstart
          name: Install required tools
        - match: Install the Knative quickstart plugin
          name: Install the Knative quickstart plugin
          description: The plugin sets up Knative against kind by creating a kind cluster populated with Knative
        - Run the Knative quickstart plugin
codeblocks:
    # validation for step 2: install the knative quickstart plugin
    - match: ^brew install knative-sandbox/kn-plugins/quickstart$
      validate: kn quickstart --help
    - match: ^brew upgrade knative-sandbox/kn-plugins/quickstart$
      optional: true
    - match: ^kn quickstart --help$
      validate: $body
    - match: ^git clone https://github.com/knative-sandbox/kn-plugin-quickstart.git
      validate: $? -e 0 && exit 0 || exit 1
    - match: ^hack/build.sh$
      validate: $? -e 0 && exit 0 || exit 1
    - match: ^mv kn-quickstart /usr/local/bin$
      validate: kn quickstart --help
    # validation for step 3: Run the knative quickstart plugin
    - match: ^kn quickstart kind$
      validate: (kubectl cluster-info --context kind-knative) && exit 0 || exit 1
    - match: ^kn quickstart minikube$
      validate: minikube profile list
    - match: ^minikube tunnel --profile knative$
      validate: $? -e 0 && exit 0 || exit 1
---

--8<-- "https://raw.githubusercontent.com/kubernetes-sigs/kui/master/plugins/plugin-kubectl/notebooks/knative-what-is-it-good-for.md"

---

::imports

---

--8<-- "https://raw.githubusercontent.com/mra-ruiz/docs/guidebooks/docs/getting-started/README.md"

---

--8<-- "https://raw.githubusercontent.com/mra-ruiz/docs/guidebooks/docs/getting-started/quickstart-install.md"