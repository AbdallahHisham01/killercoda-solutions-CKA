## Question

Your task involves setting up storage components in a Kubernetes cluster. Follow these steps:

 - Step 1: Create a Storage Class named blue-stc-cka with the following properties:

    Provisioner: kubernetes.io/no-provisioner
    Volume binding mode: WaitForFirstConsumer

 - Step 2: Create a Persistent Volume (PV) named blue-pv-cka with the following properties:

    Capacity: 100Mi
    Access mode: ReadWriteOnce
    Reclaim policy: Retain
    Storage class: blue-stc-cka
    Local path: /opt/blue-data-cka
    Node affinity: Set node affinity to create this PV on controlplane .
  
 - Step 3: Create a Persistent Volume Claim (PVC) named blue-pvc-cka with the following properties:

    Access mode: ReadWriteOnce
    Storage class: blue-stc-cka
    Storage request: 50Mi
    The volume should be bound to blue-pv-cka .

## Step 1: Create StorageClass

```
apiVersion:  storage.k8s.io/v1
kind: StorageClass
metadata:
  name: blue-stc-cka
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
```

## Step 2: Create PV

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: blue-pv-cka
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: blue-stc-cka
  local:
    path: /opt/blue-data-cka
  nodeAffinity:
     required:
        nodeSelectorTerms:
          - matchExpressions:
              - key: kubernetes.io/hostname
                operator: In
                values:
                  - controlplane
```

## Step 3: Create PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: blue-pvc-cka
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: blue-stc-cka
  volumeName: blue-pv-cka
  resources:
    requests:
      storage: 50Mi
```
