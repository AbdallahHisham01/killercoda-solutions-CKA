## Question

A Kubernetes pod definition file named nginx-pod-cka.yaml is available. Your task is to make the following modifications to the manifest file:

 - Create a Persistent Volume Claim (PVC) with the name nginx-pvc-cka . This PVC should request 80Mi of storage from an existing Persistent Volume (PV) named nginx-pv-cka and Storage Class namednginx-stc-cka . Use the access mode ReadWriteOnce .

 - Add the created nginx-pvc-cka PVC to the existing nginx-pod-cka POD definition.
 
 - Mount the volume claimed by nginx-pvc-cka at the path /var/www/html within the nginx-pod-cka POD.
 
 - Add tolerations with the key node-role.kubernetes.io/control-plane set to Exists and effect NoSchedule to the nginx-pod-cka Pod
 
 - Ensure that the nginx-pod-cka POD is running and that the Persistent Volume (PV) is successfully bound .

## Step 1: Create PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nginx-pvc-cka
spec:
  resources:
    requests:
      storage: 80Mi
  volumeName: nginx-pv-cka
  storageClassName: nginx-stc-cka
  accessModes:
    - ReadWriteOnce
```

## Step 2: Edit nginx-pod-cka POD

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod-cka
spec:
  containers:
    - name: my-container
      image: nginx:latest
      volumeMounts:
        - name: pvc
          mountPath: /var/www/html
  tolerations:
    - key: node-role.kubernetes.io/control-plane
      operator: Exists
      effect: NoSchedule
  volumes:
    - name: pvc
      persistentVolumeClaim:
        claimName: nginx-pvc-cka
```
