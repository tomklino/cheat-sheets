# Kubernetes

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
