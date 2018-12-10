
## Requirements

* Working Docker Desktop install
* `docker-app` installed
* Source code from this directory
* Create a context with `docker-app context`
* Set the `DOCKER_TARGET_CONTEXT` environment variable


## Examples

Let's install the `hello world` example. Note that this doesn't run any containers on Docker or Kubernetes, it just demonstrates the basic verbs.

```console
$ docker-app install bundle.json
Port parameter was set to 8080
Install action
Action install complete for helloworld
```

Grab the status of the application:

```console
$ docker-app status helloworld
Port parameter was set to 8080
Status action
Action status complete for helloworld
```

Finally uninstall it:

```console
$ docker-app uninstall helloworld
Port parameter was set to 8080
uninstall action
Action uninstall complete for helloworld
```


Not required, but you can show interop with `duffle` here if you're using it. For example you can list claims in Duffle and it will show applications installed via `docker-app`

```console
$ duffle claims list
helloworld
```



