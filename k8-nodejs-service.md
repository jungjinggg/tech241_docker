```yml
---
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