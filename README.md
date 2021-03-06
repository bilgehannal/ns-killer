# NS Killer

## What is NS Killer?
A Kubernetes project to kill all namespace living over X times. Quite useful when auto-generated development environments on the fly and give them a lifecycle out-of-the-box from Kubernetes or even Helm.

## Getting started
### Docker
```bash
docker run -ti -d --name=ns-killer germainlefebvre4/ns-killer
```

### Kubernetes
```bash
kubectl apply -f kubernetes/CronJob
```

## Configuration
The container has no parameters. Configuration is provided by a file at `/etc/config/ns-killer`.

Configuration file is structured as following:

| Attribute | Description | Values | Default | Implemented? |
|---|---|---|---|---|
| config.retention.kind | Time unit for the frequency loop | (string) minutes, hours, days, weeks, months | - | Yes |
| config.retention.time | Time data for the frequency loop | (integer) | - | Yes |
| config.namespace.exclude | List of namespaces to keep | list of (string) | - | Yes |
| config.namespace.only | List of namespaces to delete. This parameter make the exclude list evicted. | list of (string) | - | Yes |

### Example
```yaml
config:
  retention:
    kind: hours
    time: 2
namespace:
  exclude:
    - ns-killer
    - kube-system
    - kube-public
    - kube-node-lease
    - default
    - ingress-nginx
    - cert-manager
    - gitlab-managed-apps
    - cattle-system
    - monitoring
    - prometheus
    - jenkins
    - mongodb
    - rabbitmq-ha
    - wordpress
    - gcr-cleanup
  only: []
```

## Where to use this image
Let's run this image in a Kubernetes cluster.

Kubernetes manifest are present in directory [kubernetes/](kubernetes).
