# Deploy Sparta App on Docker and K8

## MongoDB
1. pull mongodb image version 4
   ```
   docker pull mongo:4
   ```

2. change bindip to allow all access
   ```
   docker exec -it <image-id> sh
   ```

3. update, install sudo and install nano 
   ```
   apt update
   apt install sudo
   sudo apt install nano
   ```

4. locate /etc/mongod.conf.org: change `bindIp: 27017` to `0.0.0.0`
5. commit the changes
   ```
   docker commit container-id name-of-image
   docker commit 60c1f214d83d parichanket/tech241-mongodb
   ```

6. push the image
   ```
   docker push username/custom-nginx
   docker push parichanket/tech241-parichat-nginx
   ```

7. mongodb persistent volume claim script
   ```yml
    # This file created so that even if pods gets restarted or deleted, the data wont be lost

    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
    name: mongo-db
    spec:
    accessModes:
        - ReadWriteOnce
    resources:
        requests:
        storage: 256Mi

   ```

8. mongodb deployment script
   ```yml
    apiVersion: apps/v1 # which API to use for deployment
    kind: Deployment # pod - service what kind of service you want to create
    # what would you like to call it - name the service/object
    metadata:
    name: mongo # naming the deployment
    spec:
    selector:
        matchLabels:
        app: mongo #look for this label to match with k8 service
        # let's create a replica set of this with instances/pods
    replicas: 1 # 3 pods
        # template to use it's label for k8 service to launch in the browser
    template:
        metadata:
        labels:
            app: mongo # this label connects to the service or any other k8 components
    # let's define the container spec
        spec:
        containers:
            - name: mongo
            image: parichanket/mongodb # use the image that you built
            ports:
                - containerPort: 27017
            volumeMounts:
                - name: storage
                mountPath: /data/db
        volumes:
            - name: storage
            persistentVolumeClaim:
                claimName: mongo-db
   ```

9.  mongodb service script
    ```yml
    apiVersion: v1
    kind: Service
    metadata:
    name: mongo
    spec:
    selector:
        app: mongo
    ports:
        - port: 27017
        targetPort: 27017
    ```

10. nodejs app deployment script
    ```yml
    apiVersion: apps/v1 # which API to use for deployment
    kind: Deployment # pod - service what kind of service you want to create
    # what would you like to call it - name the service/object
    metadata:
    name: node # naming the deployment
    spec:
    selector:
        matchLabels:
        app: node #look for this label to match with k8 service
        # let's create a replica set of this with instances/pods
    replicas: 3 # 3 pods
        # template to use it's label for k8 service to launch in the browser
    template:
        metadata:
        labels:
            app: node # this label connects to the service or any other k8 components
    # let's define the container spec
        spec:
        containers:
            - name: node
            image: parichanket/tech241-nodejs-app:v1 # use the image that you built
            ports:
                - containerPort: 3000
            env:
                - name: DB_HOST
                value: mongodb://mongo:27017/posts
            imagePullPolicy: Always
    ```

11. nodejs app service script
    ```yml
    # select the type of api version and type of service/object
    apiVersion: v1
    kind: Service

    # Metadata for name
    metadata:
    name: nodejs-app-service
    # sre
    namespace: default 

    # Specification to include ports selector to conect to the deployment
    spec:
    ports:
    # range: 30000 - 32768
    - nodePort: 30002
        port: 3000
        targetPort: 3000

    # define the selector and label to connect to nginx deployment
    selector:
        # label connects this service to deployment
        app: nodejs-app

    # Create nodeport type of deployment
    # also use loadbalancer - for local use cluster IP
    type: NodePort
    ```

11. run the scripts
    ```
    kubectl create -f mongodb-pvc.yml
    kubectl create -f mongodb-deploy.yml
    kubectl create -f mongodb-service.yml
    kubectl create -f nodejs-deploy.yml
    kubectl create -f nodejs-service.yml
    ```

12. if changes are made, command to apply changes
    ```
    kubectl apply -f <file-name>
    ```