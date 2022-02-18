# Deploying your Knative Service

The "Hello world" Service will be deployed as a Knative Service, not a Kubernetes Service.

This service will accept an environment variable, `TARGET`, and print "`Hello ${TARGET}!`." If `TARGET` is not specified, World will be used as the default value.

## Knative Service: "Hello world!"
=== "kn"

    ``` bash
    kn service create hello \
    --image gcr.io/knative-samples/helloworld-go \
    --port 8080 \
    --env TARGET=World \
    --revision-name=world
    ```

    ??? question "Why did I pass in `revision-name`?"
        Note the name "world" which you passed in as "revision-name," naming your `Revisions` will help you to more easily identify them

=== "YAML"
    1. Create a new file, `service.yaml` and copy the following service definition into the file.

        ``` yaml
        apiVersion: serving.knative.dev/v1
        kind: Service
        metadata:
          name: hello
        spec:
          template:
            metadata:
              # This is the name of our new "Revision," it must follow the convention {service-name}-{revision-name}
              name: hello-world
            spec:
              containers:
                - image: gcr.io/knative-samples/helloworld-go
                  ports:
                    - containerPort: 8080
                  env:
                    - name: TARGET
                      value: "World"
        ```

    1. Deploy the Knative Service by running the command:

        ``` bash
        kubectl apply -f hello.yaml
        ```
        ??? question "Why did I pass in the second name, `hello-world`?"
            Note the name `hello-world` which you passed in under `metadata` in your YAML file. Naming your `Revisions` will help you to more easily identify them, but don't worry if this if a bit confusing now, you'll learn more about `Revisions` later.

    1. To see the URL where your Knative Service is hosted, leverage the `kn` CLI:

        ```bash
        kn service list
        ```

    1. Run the following command to find the domain URL for your service:

      ```bash
      kubectl get ksvc helloworld-go  --output=custom-columns=NAME:.metadata.name,URL:.status.url
      ```

    After your service is created, Knative will perform the following steps:

      - Create a new immutable revision for this version of the app.
      - Network programming to create a route, ingress, service, and load balance
        for your app.
      - Automatically scale your pods up and down (including to zero active pods).

## Ping your Knative Service
Ping your Knative Service by opening [http://hello.default.127.0.0.1.sslip.io](http://hello.default.127.0.0.1.sslip.io){target=_blank} in your browser of choice or by running the command:

```bash
curl http://hello.default.127.0.0.1.sslip.io
```

??? question "Are you seeing `curl: (6) Could not resolve host: hello.default.127.0.0.1.sslip.io`?"

    In some cases your DNS server may be set up not to resolve `*.sslip.io` addresses. If you encounter this problem, it can be fixed by using a different nameserver to resolve these addresses.

    The exact steps will differ according to your distribution. For example, with Ubuntu derived systems which use `systemd-resolved`, you can add the following entry to the `/etc/systemd/resolved.conf`:

    ```ini
    [Resolve]
    DNS=8.8.8.8
    Domains=~sslip.io.
    ```

    Then simply restart the service with `sudo service systemd-resolved restart`.

    For MacOS users, you can add the DNS and domain using the network settings as explained [here](https://support.apple.com/en-gb/guide/mac-help/mh14127/mac).