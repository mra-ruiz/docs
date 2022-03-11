---
title: Autoscaling Using Go
layout:
    1: left
    default: wizard
wizard:
    steps:
        - match: Prerequisites
          name: Install Required Tools
        - name: Deploy the Service
        - name: Load the Service
        - match: Analysis
          name: Analysis - Algorithm
        - name: Other Experiments
          describe: Run experiments to better understand analysis
        - name: Cleanup
        - name: Further reading
codeblocks:
    # Validation for Step 1: Install Required Tools
    - match: ^git clone -b "{{ branch }}" https://github.com/knative/docs knative-docs
          cd knative-docs$
      validate: $? -e 0 && exit 0 \|\| exit 1
    # Validation for Step 2: Building your application
    - match: ^kubectl apply -f docs/serving/autoscaling/autoscale-go/service.yaml$
      validate: kn service describe service
    - match: ^ \$ kubectl apply
      optional: true
    # Validation for Step 3: Load the Service
    - match: ^curl "http://autoscale-go.default.1.2.3.4.sslip.io?sleep=100&prime=10000&bloat=5"$
      validate: $body
---

--8<-- "https://raw.githubusercontent.com/kubernetes-sigs/kui/master/plugins/plugin-kubectl/notebooks/knative-what-is-it-good-for.md"

---

--8<-- "docs/serving/autoscaling/autoscale-go/README.md"