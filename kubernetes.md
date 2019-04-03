# Kubernetes

## Common

* Executing a pod as an interactive shell

```bash
kubectl run --generator=run-pod/v1 --rm -i --tty busybox --image=busybox -- sh
```

* Executing a shell in a pod:

```bash
kubectl exec -it pod-name -- /bin/bash
```

* Getting the worker node running a specific pod

```bash
kubectl get pod <pod-name> -o custom-columns=Name:{.metadata.name},Node:{.spec.nodeName}
```

## Useful custom-colomns:

* get node name for pod:

```
custom-columns=Name:{.metadata.name},Node:{.spec.nodeName}
```

* get memory requests and limits for each container in pod

```
custom-columns=Name:{.metadata.name},Requests:{.spec.containers[*].resources.requests.memory},Limits:{.spec.containers[*].resources.limits.memory}```

## Advanced label search

* Search a resource that matches label.a AND label.b

```bash
kubectl get pod -l label.a=value1,label.b=value2
```

* Search a resource that matches label.a OR label.b

```bash
kubectl get pod -l label.a=value1 -l label.b=value2
```

## Secrets

* Creating a secret

```bash
kubectl create secret generic name-of-secret --from-file=/path/to/file
```

## Parsing tricks

* Getting the selectors for a service:

```bash
kubectl get svc name-of-service -o json | jq '.spec.selector'
```

* Get owner of a pod by label:

```bash
kubectl get pod -l label=something -o json | jq -C '.items[] | { name: .metadata.name, owner: { kind: .metadata.ownerReferences[].kind, name: .metadata.ownerReferences[].name } } '
```