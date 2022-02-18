---
title: Installing Knative
---

# Installing Knative

You can install the Serving component, Eventing component, or both on your
cluster by using one of the following deployment options:

=== "Knative Quickstart plugin"

    Use the [Knative Quickstart plugin](install-knative-quickstart.md) to install a preconfigured, local distribution of Knative for development purposes. 

=== "YAML-based installation"

    Use a YAML-based installation to install a production ready deployment:
        - [Install Knative Serving by using YAML](../install/yaml-install/serving/install-serving-with-yaml.md)
        - [Install Knative Eventing by using YAML](../install/yaml-install/eventing/install-eventing-with-yaml.md)

=== "Knative Operator"

    Use the [Knative Operator](knative-with-operators.md) to install and configure a production ready deployment.
    
=== "Knative offerings"
    Follow the documentation for vendor managed [Knative offerings](knative-offerings.md).
    
!!! note
    You can also [upgrade an existing Knative installation](docs/install/upgrade/README.md). Knative installation instructions assume you are running Mac or Linux with a bash shell.