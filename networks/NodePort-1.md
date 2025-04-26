## Question

Create a deployment named my-web-app-deployment using the Docker image wordpress with 2 replicas. Then, expose the my-web-app-deployment as a service named my-web-app-service , making it accessible on port 30770 on the nodes of the cluster.

## Step 1: Create Dep

```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: my-web-app-deployment
  name: my-web-app-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-web-app-deployment
  template:
    metadata:
      labels:
        app: my-web-app-deployment
    spec:
      containers:
      - image: wordpress
        name: wordpress
        ports:
          - containerPort: 80
            name: http
            protocol: TCP
```

## Step 2: Create SVC

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: my-web-app-deployment
  name: my-web-app-service
spec:
  ports:
  - nodePort: 30770
    protocol: TCP
    targetPort: 80
    port: 80
  selector:
    app: my-web-app-deployment
  type: NodePort
```
