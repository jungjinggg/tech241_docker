```yml
# which api to use for deployment
apiVersion: apps/v1

# pod - service what kind of service/object to create
kind: Deployment

metadata:
  # naming the deployment
  name: nginx-deployment

spec:
  selector:
    matchLabels:
      # look for this label to match with k8 service
      app: nginx

  # create a replica set with instances/pods
  # 3 pods
  replicas: 3 

  # template to use its label for k8 service to launch in the browser
  template:
    metadata:
      labels:
        # this label connects to the service or any other k8 components
        app: nginx
    
    # define the container spec
    spec:
      containers:
      - name: nginx
        image: parichanket/tech241-nginx:v1
        ports:
        - containerPort: 80

```

To create pods
```
kubectl create -f <file-name>
kubectl create -f nginx-deploy.yml
```

Check the deployment
```
kubectl get deploy
```

Check the pods
```
kubectl get pods
```