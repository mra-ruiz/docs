---
title: Installing Knative
---

# Installing Knative

You can install the Serving component, Eventing component, or both on your
cluster by using one of the following deployment options:

=== "Knative Quickstart plugin"

    Use the [Knative Quickstart plugin](../guidebooks/install-knative-quickstart.md) to install a preconfigured, local distribution of Knative for development purposes.

    :import{docs/guidebooks/install-knative-quickstart.md}

=== "YAML-based installation"

    Use a YAML-based installation to install a production ready deployment:
        - [Install Knative Serving by using YAML](../install/yaml-install/serving/install-serving-with-yaml.md)
        - [Install Knative Eventing by using YAML](../install/yaml-install/eventing/install-eventing-with-yaml.md)

    :import{docs/install/yaml-install/serving/install-serving-with-yaml.md}
    :import{docs/install/yaml-install/eventing/install-eventing-with-yaml.md}

=== "Knative Operator"

    Use the [Knative Operator](operator/knative-with-operators.md) to install and configure a production ready deployment.
    
    :import{docs/install/operator/knative-with-operators.md}

=== "Knative offerings"

    Follow the documentation for vendor managed [Knative offerings](knative-offerings.md).
    
    :import{docs/install/knative-offerings.md}

!!! note

    Knative installation instructions assume you are running Mac or Linux with a bash shell.
    
    <!-- TODO: Link to provisioning guide for advanced installation -->
    
    You can also [upgrade an existing Knative installation](docs/install/upgrade/README.md). Knative installation instructions assume you are running Mac or Linux with a bash shell.