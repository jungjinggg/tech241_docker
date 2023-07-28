# Kubernetes (K8)
Kubernetes is an open source system to deploy, scale and manage containerised applications anywhere. K8 provides a rich set of features that enable developers and operations teams to efficiently manage containerised workload.

## K8 Architecture
The architecture is based on a master-worker model.
1. Master Node is responsible for managing the cluster and its components. 
2. Worker Nodes are the nodes where containers are deployed and run.
   
![K8 Architecture](images/k8-arch.jpg)

## Why K8?
It provides scalability where it enables horizontal scaling of applications to handle increased traffic and demand efficiently. Also, K8 ensrures that applications are always available by autometically managing and recovering failed containers and nodes. Importantly, K8 automates the deployment, scaling and management of containerised applications.

## Who uses K8?
K8 is widely used across various industries and organisations.
* Google
* Microsoft
* Amazon Web Service (AWS)
* Netflix
* Spotify

## Business Values
Kubernetes offers faster deployment where it accelerates the deployment process allowing the business to release features and updates quickly and reliably.

## K8 Objects
Objects are the building blaocks used to define the desired state of the cluster.

1. Pods are the smallest deployable units which represents one or more containers that are tightly coupled and share the same network namespace and storage
2. Deployments are used to manage the desired state of replica sets and pods.
3. Services enable communication between different sets and pods.
4. ReplicaSets are used to ensure that a specified number of replicas of a pod are running. It also replaces and scales pods when required.

## Concept of Labels and Selectors
* Labels: key-value pairs which are used to organise and identify objects.
* Selectors: used to identify a set of objects based on their labels
  
