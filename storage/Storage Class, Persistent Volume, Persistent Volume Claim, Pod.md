## Question

 - Create a Storage Class named fast-storage with a provisioner of kubernetes.io/no-provisioner and a volumeBindingMode of Immediate .

 - Create a Persistent Volume (PV) named fast-pv-cka with a storage capacity of 50Mi using the fast-storage Storage Class with ReadWriteOnce permission and host path /tmp/fast-data .

 - Create a Persistent Volume Claim (PVC) named fast-pvc-cka that requests 30Mi of storage from the fast-pv-cka PV(using the fast-storage Storage Class).

 - Create a Pod named fast-pod-cka with nginx:latest image that uses the fast-pvc-cka PVC and mounts the volume at the path /app/data .

## Step 1: Create StorageClass

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: Immediate
```

## Step 2: Create PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: fast-pvc-cka
spec:
  resources:
    requests:
      storage: 30Mi
  storageClassName: fast-storage
  accessModes:
    - ReadWriteOnce
```

## Step 3: Create PV

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: fast-pv-cka
spec:
  capacity:
    storage: 50Mi
  accessModes:
    - ReadWriteOnce
  storageClassName: fast-storage
  hostPath:
    path: /tmp/fast-data
```

## Step 4: Create Pod

```
apiVersion: v1
kind: Pod
metadata:
  name: fast-pod-cka
spec:
  containers:
  - image: nginx:latest
    name: my-container

    volumeMounts:
      - mountPath: /app/data
        name: fast-pvc-cka

  volumes:
    - name: fast-pvc-cka
      persistentVolumeClaim:
        claimName: fast-pvc-cka
```

## Step 5: Apply The Configurations

```
kubectl apply -f storageclass.yml
kubectl apply -f pvc.yml
kubectl apply -f pv.yml
kubectl apply -f pod.yml
```
