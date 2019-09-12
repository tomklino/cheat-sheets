# Kubernetes

## Emergencies

* Rollback helm to previos successful release

```bash
helm rollback <release-name> 0
```

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

* Get all pending pods

```bash
kubectl get pods --field-selector=status.phase=Pending
```

* Get all pods scheduled to a specific node:

```bash
kubectl get pods --all-namespaces --field-selector spec.nodeName=worker1
```

* Get events for a specific pod

```bash
kubectl get events --field-selector=involvedObject.name=<pod-name>
```

## Useful custom-colomns:

* get node name for pod:

```
custom-columns=Name:{.metadata.name},Node:{.spec.nodeName}
```

* get owner of each pod:
```
custom-columns=Name:{.metadata.name},Owner:{.metadata.ownerReferences[].name}
```

* get ip for each pod:
```
custom-columns=Name:{.metadata.name},IP:{.status.podIP}
```

* get images of containers for each pod:
```
custom-columns=Name:{.metadata.name},Image:{.spec.containers[].image}
```

* get memory requests and limits for each container in pod

```
custom-columns=Name:{.metadata.name},Requests:{.spec.containers[*].resources.requests.memory},Limits:{.spec.containers[*].resources.limits.memory}
```

## Resizing Stateful Sets PVC with no down-time (works for increasing only)

 1. Edit the helm values.yaml or the sts template accordingly
 2. Delete the sts with an arg --cascade=false
 3. Apply the chart or the new sts
 4. Manually edit the existing pvcs to the new size
 5. After about 30 seconds, restart the sts pods one by one

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

## Minikube

* Attaching a directory from the workstation directly to a pod

1. mount the dir into minikube with minikube mount (e.g. `minikube mount $(pwd):/go-dev`)
2. create a pod that utilizes a volume as a hostpath to the destination mounted in step 1:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: go-dev
spec:
  containers:
  - name: go-dev
    image: 'golang:1.12-stretch'
    stdin: true
    tty: true
    args: [ "bash" ]
    workingDir: '/app'
    volumeMounts:
      - mountPath: '/app'
        name: "host-mount"
  volumes:
    - name: "host-mount"
      hostPath:
        path: "/go-dev"
```
3. execute or attach into the pod `kubectl exec -it go-dev -- bash`
