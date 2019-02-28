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
