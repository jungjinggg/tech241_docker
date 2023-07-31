```yml
# which api to use for deployment
apiVersion: apps/v1

# pod - service what kind of service/object to create
kind: Deployment

metadata:
  # naming the deployment
  name: nodejs-app-deployment

spec:
  selector:
    matchLabels:
      # look for this label to match with k8 service
      app: nodejs-app

  # create a replica set with instances/pods
  # 3 pods
  replicas: 3 

  # template to use its label for k8 service to launch in the browser
  template:
    metadata:
      labels:
        # this label connects to the service or any other k8 components
        app: nodejs-app
    
    # define the container spec
    spec:
      containers:
      - name: nodejs-app
        image: parichanket/tech241-nodejs-app:v1
        ports:
        - containerPort: 3000

```