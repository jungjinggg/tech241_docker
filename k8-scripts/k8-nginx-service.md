```yml
---
# select the type of api version and type of service/object
apiVersion: v1
kind: Service

# Metadata for name
metadata:
  name: nginx-svc
  # sre
  namespace: default 

# Specification to include ports selector to conect to the deployment
spec:
  ports:
  # range: 30000 - 32768
  - nodePort: 30001
    port: 80
    targetPort: 80

# define the selector and label to connect to nginx deployment
  selector:
    # label connects this service to deployment
    app: nginx

  # Create nodeport type of deployment
  # also use loadbalancer - for local use cluster IP
  type: NodePort
```

To create a service
```
kubectl create -f <file-name>
kubectl create -f nginx-service.yml
```

Ckeck the service
```
kubectl get svc
```