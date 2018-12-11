# Docker App CNAB examples

This examples in this repository show some basic examples of using `docker-app`, in particular showing some of the CNAB integration details.Feel free to work through each of the examples in order, pick and choose, or modify for your own application.

* [A simple Compose Hello World example](https://github.com/garethr/docker-app-cnab-examples/tree/master/app1)
* [pushing a CNAB to Docker Hub](https://github.com/garethr/docker-app-cnab-examples/tree/master/app2)
* [CNAB hello world example](https://github.com/garethr/docker-app-cnab-examples/tree/master/app3)
* [Installing a Helm chart using Docker App and CNAB](https://github.com/garethr/docker-app-cnab-examples/tree/master/app4)


## Detailed setup instructions

Most of this work is moving quickly so official installation instructions and packages will come later. If you need to run these demos you'll need to do some setup. The following instructions should help.

### Docker App

Binaries for both Docker App can be downloaded here: https://github.com/docker/app/releases/
Take the binaries you need, rename them to `docker-app` (or `docker-app.exe` on Windows) and and put them somewhere in your PATH

### Credentials

`docker-app` uses the new Docker Context functionality which will be available in a future version of Docker. For the moment it bundles this in the `docker-app` CLI itself.

Docker Desktop exposes a Kubernetes cluster on localhost, but trying to access that cluster on localhost from within a container will fail. This means you probably need to create a separate Kubernetes context. Copy your existing context (in `~/.kube/config`) and then replace the following content:

```diff
- server: https://localhost:6445
+ server: https://192.168.65.3:6443
```

With that done you should be able to run the following, pointing at the file you just created with the modified server address.

```console
$ docker-app context create local --default-stack-orchestrator=kubernetes --description="Local Kubernetes and Docker" --docker-host=unix:///var/run/docker.sock --kubernetes-kubeconfig=<absolute path to kubeconfig>
```

You can pass the context to all the `docker-app` commands but that gets tedious quickly. Instead lets set an environment variable pointing at the context you just created.

```powershell
$Env:DOCKER_TARGET_CONTEXT="local"
```

```bash
export DOCKER_TARGET_CONTEXT=local
```


### Duffle

Some examples also use `duffle`, the CNAB reference client. This can be downloaded from https://github.com/deislabs/duffle/releases. Once you have `duffle` installed you should run the following to create various directories and files.

```console
duffle init
```

Create a credentials file that points to your modified Kubernetes context. Note that it needs to be a absolute path, so
modify the following as appropriate. Save as `local.yaml`

```yaml
name: local
credentials:
  - name: kubeconfig
    source:
      path: C:\Users\garet\.kube\desktop
```

The add those credentials to the duffle store:

```console
duffle credentials add local.yaml
```

Additionaly, if you want to create a credentialset suitable for manipulating docker-app based packages with duffle, you can run:

```
docker-app add-credentialset <duffle credentialset name> <docker context name>
``` 


### Helm

Helm installation instructions for the Helm demo can be found on [helm.sh](https://helm.sh/). With Helm installed you'll want to install Tiller with the following:

```console
$ helm init
$HELM_HOME has been configured at C:\Users\garet\.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.

Please note: by default, Tiller is deployed with an insecure 'allow unauthenticated users' policy.
To prevent this, run `helm init` with the --tiller-tls-verify flag.
For more information on securing your installation see: https://docs.helm.sh/using_helm/#securing-your-helm-installation
Happy Helming!
```
