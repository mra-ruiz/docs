---
hide_next: true
---
# Clean Up

We recommend that you delete the cluster used for this tutorial to free up resources
on your local machine.

If you want to continue experimenting with Knative after deleting the cluster,
you can reinstall Knative on a new cluster using the [`quickstart` plugin](quickstart-install.md#run-the-knative-quickstart-plugin) again.

## Delete the Cluster

=== "kind"

    Delete your `kind` cluster by running the command:

    ```bash
    ---
    validate: (kubectl cluster-info --context kind-knative) && exit 1 || exit 0
    ---
    kind delete clusters knative
    ```

=== "minikube"

    Delete your `minikube` cluster by running the command:

    ```bash
    ---
    optional: True
    validate: (kubectl cluster-info --context kind-knative) && exit 1 || exit 0
    ---
    minikube delete -p knative
    ```
