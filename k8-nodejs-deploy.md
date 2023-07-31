```yml
# which api to use for deployment
apiVersion: apps/v1
# pod - service what kind of service you want to create
kind: Deployment 
# what would you like to call it - name the service/object
metadata:
  # naming the deployment
  name: node 
spec:
  selector:
    matchLabels:
      #look for this label to match with k8 service
      app: node 
  # let's create a replica set of this with instances/pods
   # 3 pods
  replicas: 3
  # template to use it's label for k8 service to launch in the browser
  template:
    metadata:
      labels:
        # this label connects to the service or any other k8 components
        app: node 
  # let's define the container spec
    spec:
      containers:
        - name: node
          # the image that you built
          image: parichanket/tech241-nodejs-app 
          ports:
            - containerPort: 3000
          env:
            - name: DB_HOST
              value: mongodb://mongo:27017/posts
          imagePullPolicy: Always
```