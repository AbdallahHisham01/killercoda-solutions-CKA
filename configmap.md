## Question 1

- Create a ConfigMap named trauerweide with content tree=trauerweide
- Create the ConfigMap stored in existing file /root/cm.yaml

## Solution

```
kubectl create configmap trauerweide --from-literal tree=trauerweide --dry-run=client -o yaml > cm.yaml
```

## Question 2

- Create a Pod named pod1 of image nginx:alpine
- Make key tree of ConfigMap trauerweide available as environment variable TREE1
- Mount all keys of ConfigMap birke as volume. The files should be available under /etc/birke/*
- Test env+volume access in the running Pod

## Solution

```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
  - image: nginx:alpine
    name: pod1
    env:
      - name: TREE1
        valueFrom:
          configMapKeyRef:
            key: tree
            name: trauerweide
    volumeMounts:
      - name: birke
        mountPath: /etc/birke
  volumes:
    - name: birke
      configMap:
        name: birke
  ```
