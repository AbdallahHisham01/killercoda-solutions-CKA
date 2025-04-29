## Question

Find the Pod with the highest priority in Namespace management and delete it.

## Solution

```
kubectl get pods -n management -o yaml | grep prio ## search for the highest priority

kubectl delete pod -n management sprinter
```

## Question

In Namespace lion there is one existing Pod which requests 1Gi of memory resources.

That Pod has a specific priority because of its PriorityClass.

Create new Pod named important of image nginx:1.21.6-alpine in the same Namespace. It should request 1Gi memory resources.

Assign a higher priority to the new Pod so it's scheduled instead of the existing one.

Both Pods won't fit in the cluster.

## Solution

```
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: important
  name: important
  namespace: lion
spec:
  containers:
  - image: nginx:1.21.6-alpine
    name: important
    resources:
      requests:
        memory: 1Gi
  priorityClassName: level3
```
