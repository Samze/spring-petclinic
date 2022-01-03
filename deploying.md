
# Deployment with skaffold

## Build the application and deploy to Kubernetes

For a local cluster like Minikube or Docker Desktop you can simply run:

```bash
skaffold run --port-forward --profile=local --tail
```

For a remote cluster you need to specify the `default-repo` which is the registry prefix for the image that is being built. For Docker Hub the prefix would be your Docker ID, for other registries it would typically be the registry URL plus your project.

> **NOTE**: You must specify a registry prefix where you have permission to push images.

You can do this globally by running:

```bash
skaffold config set --global default-repo ${REGISTRY_PREFIX}
```

Or, you can set it for the current Kubernetes context:

```bash
skaffold config set default-repo ${REGISTRY_PREFIX}
```

Finally, you can specify it as part of the `run` command:

```bash
skaffold run --default-repo ${REGISTRY_PREFIX} --port-forward --tail
```

The `skaffold run` command will build the container image, deploy the application and port-forward the service to `localhost:8080`

Open another terminal window to interract with the application or Kubernetes API server.

You can use `kubectl get all` to verify that the resources were created.

If you leave out the `--port-forward` option then accessing the application's endpoint varies based on the type of Kubernetes cluster and ingress configuration you are using.

## Delete the application

To delete the deployment and the service from your Kubernetes cluster run:

```bash
skaffold delete
```