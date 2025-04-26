## Question

An existing nginx pod, my-pod-cka and Persistent Volume Claim (PVC) named my-pvc-cka are available. Your task is to implement the following modifications:

 - NOTE:- PVC to PV binding and my-pod-cka pods sometimes takes around 2Mins to Up & Running So Please wait

 - Update the pod to include a sidecar container that uses the busybox image. Ensure that this sidecar container remains operational by including an appropriate command "tail -f /dev/null" .

 - Share the shared-storage volume between the main application and the sidecar container, mounting it at the path /var/www/shared . Additionally, ensure that the sidecar container has read-only access to this shared volume.

## Step 1: Export the Existing Pod Configuration

```
kubectl get pod my-pod-cka -o yaml > pod.yml
```

## Step 2: Edit the Pod YAML to Add a Sidecar Container

```
 - name: sidecar-container
    image: busybox
    volumeMounts:
      - mountPath: /var/www/shared
        readOnly: true
        name: shared-storage
    command: ["sh", "-c", "tail","-f","/dev/null"]
```

## Step 3: Apply the Updated Pod Configuration

```
kubectl replace -f pod.yml --force
```
