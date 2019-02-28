# Kubernetes

## Advanced label search

* Search a resource that matches label.a AND label.b

```bash
kubectl get pod -l label.a=value1 label.b=value2
```

* Search a resource that matches label.a OR label.b

```bash
kubectl get pod -l label.a=value1 -l label.b=value2
```

* Creating a secret

```bash
kubectl create secret generic name-of-secret --from-file=/path/to/file
```
* Executing a shell in a pod:

```bash
kubectl exec -it pod-name -- /bin/bash
```

* Getting the selectors for a service:

```bash
kubectl get svc name-of-service -o json | jq '.spec.selector'
```

* Get owner of a pod by label:

```bash
kubectl get pod -l label=something -o json | jq -C '.items[] | { name: .metadata.name, owner: { kind: .metadata.ownerReferences[].kind, name: .metadata.ownerReferences[].name } } '
```
