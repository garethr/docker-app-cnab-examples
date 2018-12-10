## Requirements

* Working Docker Desktop install with Kubernetes enabled
* `docker-app` installed
* Source code from this directory
* Create a context with `docker-app context`
* Set the `DOCKER_TARGET_CONTEXT` environment variable


## Examples


First take a look at the application locally:

```console
$ docker-app inspect
monitoring 0.1.0

Maintained by: Gareth Rushgrove <garethr@docker.com>

A basic prometheus stack

Services (2) Replicas Ports Image
------------ -------- ----- -----
prometheus   1        9090  prom/prometheus:latest
alertmanager 1        9093  prom/alertmanager:latest

Parameters (4)        Value
--------------        -----
ports.alertmanager    9093
ports.prometheus      9090
versions.alertmanager latest
versions.prometheus   latest
```

Let's now push that application to Docker Hub for sharing.

```console
docker-app push --namespace <your-namespace>
```

For the next set of examples we don't need the local files, in fact this could be on another machine entirely.

Let's inspect the application again:

```console
docker-app inspect <your-namespace>/monitoring:0.1.0
```

And then install the application from Hub.

```console
docker-app install <your-namespace>/monitoring:0.1.0
```



