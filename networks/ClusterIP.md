## Question

Create a NodePort service named app-service-cka (with below specification) to expose the nginx-app-cka deployment in the nginx-app-space namespace.

 - port & target port 80
 - protocol TCP
 - node port 31000

## Step 1: Create SVC

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: nginx-app-cka
  name: app-service-cka
  namespace: nginx-app-space
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 31000
  selector:
    app: nginx-app-cka
  type: NodePort
```
