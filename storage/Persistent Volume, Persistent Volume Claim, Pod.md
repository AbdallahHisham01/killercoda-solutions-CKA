## Question

You are responsible for provisioning storage for a Kubernetes cluster. Your task is to create a PersistentVolume (PV), a PersistentVolumeClaim (PVC), and deploy a pod that uses the PVC for shared storage.

Here are the specific requirements:

 - Create a PersistentVolume (PV) named my-pv-cka with the following properties:

   - Storage capacity: 100Mi
   - Access mode: ReadWriteOnce
   - Host path: /mnt/data
   - Storage class: standard
     
 - Create a PersistentVolumeClaim (PVC) named my-pvc-cka to claim storage from the my-pv-cka PV, with the following properties:
   -  Storage class: standard
   - request storage: 100Mi (less than)
 - Deploy a pod named my-pod-cka using the nginx container image.
 - Mount the PVC, my-pvc-cka , to the pod at the path /var/www/html . Ensure that the PV, PVC, and pod are successfully created, and the pod is in a Running state.

Note: Binding and Pod might take time to come up, please have patience

## Step 1: Create PV

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv-cka
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data
  storageClassName: standard
```

## Step 2: Create PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc-cka
spec:
  storageClassName: standard
  resources:
    requests: 
      storage: 100Mi
  accessModes:
    - ReadWriteOnce
```

## Step 3: Create POD

```
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: my-pod-cka
  name: my-pod-cka
spec:
  containers:
  - image: nginx
    name: my-container
    volumeMounts:
       - name: pvc
         mountPath: /var/www/html
  volumes:
   - name: pvc
     persistentVolumeClaim:
       claimName: my-pvc-cka
```
