# Kubernetes: From Zero to Hero

## What is Kubernetes?

Kubernetes (also known as K8s) is an open-source container orchestration platform(infact much more than just an orchestrator) designed to automate the deployment, scaling, and management of containerized applications.

---

## Why Kubernetes?

- **Orchestration**: Automatically manage and schedule containers.(helps us in deploying and manging containers dynamically)
- **Scalability**: Easily scale applications up or down.
- **Self-healing**: Automatically replaces failed containers.
- **Load Balancing**: Distributes network traffic effectively.
- **Rolling Updates & Rollbacks**: Update applications with zero downtime.
-

---

## Core Concepts

### Kubernetes Cluster 
   it is just collection of worker nodes(simply just a server) and Control plane(which was previously known as master node).

### Node
A worker machine where containers are deployed. It can be a virtual or physical machine.

### Pod
The smallest deployable/Scheduling unit in Kubernetes. A Pod can contain one or more containers.

### Service
An abstraction that defines a logical set of Pods and a policy by which to access them.

### Deployment
Manages the deployment and scaling of a set of Pods.

---

## Installation

### Minikube (Local Setup)
Minikube lets you run Kubernetes locally.

#### Prerequisites:
- VirtualBox or Docker
- kubectl CLI

#### Install Minikube:

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
Start Minikube:
    
    
    
# minikube start
Install kubectl:
    
    
    
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl


# Basic kubectl Commands
    
    
    
kubectl version                       # Show version info
kubectl cluster-info                  # Show cluster info
kubectl get nodes                     # List nodes
kubectl get pods                      # List all pods
kubectl get deployments               # List deployments
kubectl describe pod <pod-name>       # Describe a specific pod
kubectl logs <pod-name>               # View pod logs
kubectl delete pod <pod-name>         # Delete a pod



## Deploying an App
# Sample Deployment YAML
    
    
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: hello
  template:
    metadata:
      labels:
        app: hello
    spec:
      containers:
        - name: hello-container
          image: nginx
          ports:
            - containerPort: 80


# Apply the Deployment
      
    
kubectl apply -f deployment.yaml


# Create a Service
'''yaml''' 
    
    
apiVersion: v1
kind: Service
metadata:
  name: hello-service
spec:
  type: NodePort
  selector:
    app: hello
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30001
    
    
    
kubectl apply -f service.yaml

# Access the app in the browser:
    
    
http://<minikube-ip>:30001


## Namespaces
# Namespaces help organize resources within the cluster.

    
    
    
kubectl create namespace dev
kubectl get namespaces
kubectl apply -f app.yaml --namespace=dev

## ConfigMaps and Secrets
# ConfigMap  
    
kubectl create configmap app-config --from-literal=APP_ENV=production
kubectl get configmaps


# Secret
    
    
    
kubectl create secret generic app-secret --from-literal=DB_PASSWORD=pass123
kubectl get secrets
Volumes
yaml
    
    
apiVersion: v1
kind: Pod
metadata:
  name: volume-demo
spec:
  containers:
    - name: app
      image: nginx
      volumeMounts:
        - name: html
          mountPath: /usr/share/nginx/html
  volumes:
    - name: html
      hostPath:
        path: /data
        type: Directory
