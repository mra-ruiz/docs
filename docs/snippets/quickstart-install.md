# Install Knative using quickstart

This topic describes how to install a local deployment of Knative Serving and
Eventing using the Knative `quickstart` plugin. The plugin installs a preconfigured Knative deployment on a local Kubernetes cluster.

!!! warning
    Knative `quickstart` environments are for experimentation use only.
    For a production ready installation, see the [YAML-based installation](/docs/install/yaml-install/)
    or the [Knative Operator installation](/docs/install/operator/knative-with-operators/).

## Required tools

Before you can get started with a Knative `quickstart` deployment you must install:

--8<-- "https://raw.githubusercontent.com/mra-ruiz/docs/main/docs/snippets/docker-guidebook.md"

--8<-- "https://raw.githubusercontent.com/mra-ruiz/docs/main/docs/snippets/kind-guidebook.md"

--8<-- "https://raw.githubusercontent.com/mra-ruiz/docs/main/docs/snippets/kubectl-guidebook.md"

--8<-- "https://raw.githubusercontent.com/mra-ruiz/docs/main/docs/snippets/kn-cli-guidebook.md"

## Install the Knative quickstart plugin

After installing the required tools, install the Knative `quickstart` plugin:

=== "Using Homebrew"

    For macOS, install the `quickstart` plugin by using [Homebrew](https://brew.sh){target=_blank}:

    ```bash
    ---
    validate: kn quickstart --help
    ---
    brew install knative-sandbox/kn-plugins/quickstart
    ```

    Upgrade an existing install to the latest version by running the command:

    ```bash
    ---
    optional: true
    ---
    brew upgrade knative-sandbox/kn-plugins/quickstart
    ```
    
=== "Using a binary"

    1. Download the executable binary for your system from the [`quickstart` release page](https://github.com/knative-sandbox/kn-plugin-quickstart/releases){target=_blank}.

    1. Move the executable binary file to a directory on your `PATH`, for example, in `/usr/local/bin`.

    1. Verify that the plugin is working, for example:

        ```bash
        ---
        validate: $body
        ---
        kn quickstart --help
        ```

=== "Using Go"

    1. Check out the `kn-plugin-quickstart` repository:

        ```bash
        git clone https://github.com/knative-sandbox/kn-plugin-quickstart.git
        cd kn-plugin-quickstart/
        ```

    1. Build an executable binary:

        ```bash
        hack/build.sh
        ```

    1. Move the executable binary file to a directory on your `PATH`:

        ```bash
        ---
        validate: kn quickstart --help
        ---
        mv kn-quickstart /usr/local/bin
        ```

## Run the Knative quickstart plugin

The `quickstart` plugin completes the following functions:

1. Checks if you have the selected Kubernetes instance installed
1. Creates a cluster called `knative`
1. Installs Knative Serving with Kourier as the default networking layer, and sslip.io as the DNS
1. Installs Knative Eventing and creates an in-memory Broker and Channel implementation


To get a local deployment of Knative, run the `quickstart` plugin:

=== "Using kind"

    Install Knative and Kubernetes on a local Docker daemon by running:

    ```bash
    ---
    validate: (kubectl cluster-info --context kind-knative) && exit 1 || exit 0
    ---
    kn quickstart kind
    ```

=== "Using minikube"

    Install Knative and Kubernetes in a minikube instance by running:

    ```bash
    ---
    validate: minikube profile list
    ---
    kn quickstart minikube
    ```

After the plugin is finished, you should have a cluster called `knative`