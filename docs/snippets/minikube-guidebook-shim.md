---
title: Install minikube
imports:
    - docker-guidebook.md
codeblocks:
    - match: ^(minikube version >& /dev/null) && echo "You have minikube!" \|\| (echo "Please install minikube" && exit 1)$
      validate: $body
---