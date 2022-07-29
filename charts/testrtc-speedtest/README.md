# Speedtest Helm Chart
(this is a boilerplate, everytging is TBD...)

* Installs [Speedtest](https://testrtc.com/network-testing/)

## Get Repo Info

```console
helm repo add testrtc-speedtest https://bogdando.github.io/helm-charts
helm repo update
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install my-release bogdando/testrtc-speedtest
```

## Uninstalling the Chart

To uninstall/delete the my-release deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Upgrading an existing Release to a new major version

A major chart version change (like v1.2.3 -> v2.0.0) indicates that there is an
incompatible breaking change needing manual actions.

### To x.y.z example

This version requires Helm >= a.b.c.
You have to add --force to your helm upgrade command as the labels of the chart have changed.

## Configuration

| Parameter                                 | Description                                   | Default                                                 |
|-------------------------------------------|-----------------------------------------------|---------------------------------------------------------|
| `replicas`                                | Number of nodes                               | `1`                                                     |
| `image.repository`                        | Image repository                              | ``                                                      |
| `image.tag`                               | Image tag                                     | ``                                                      |
| `image.sha`                               | Image sha (optional)                          | ``                                                      |
| `image.pullPolicy`                        | Image pull policy                             | `IfNotPresent`                                          |
| `image.pullSecrets`                       | Image pull secrets (can be templated)         | `[]`                                                    |

...

### Other things

...
