# Kubernetes Ingress
---
## Introduction to Ingress
 - **Ingress** is an API object that manages **external access** to services in a Kubernetes cluster.
 - Provides:
   - **HTTP/HTTPS routing**
   - **Path-based routing** (`/app1` → Service1, `/app2` → Service2)
   - **Host-based routing** (`app1.example.com` → Service1, `app2.example.com` → Service2)
 - Ingress requires an **Ingress Controller** (commonly **NGINX Ingress Controller**).
---
<img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/a817af63-7f38-4ff0-b7df-1a306096f14a" />

---
## Notes 
### Ingress rule
 - This object ensures or rather its a rule book which states that which a user what to view a particular microservicce the traffic will diverted to that particular microservice cluster IP service object
### Ingress controller
 - Ensure that the traffic requested by the user has requested the desired destination it will route the trafic to desired destination.

| Feature | Ingress Rule |   Ingress controller |                                 
|----------|------|------|                                               
| Definition | Set of routing rules in YAML |Component that executes those rules|
| Type | Kubernetes resource (config) |Running application (pod/service)  |                     
|Written in | YAML file | Installed as software (e.g., NGINX, Traefik) |       
| Responsibility |Path/host-based routing rules |   Load balancing, SSL termination, routing |        
| Example | `/app1 → app1-service` |NGINX controller routing traffic  | 

---


## Commands
### Install kubectl 
#### Download the latest release with the command
```sh
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

#### Validate the binary
```sh
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

#### Validate the kubectl binary against the checksum file 
```sh
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

#### Install kubectl
```sh
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

#### Note: If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
```sh
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
```
```sh
kubectl version --client
```
### Create Amazon EKS cluster using eksctl
```sh
eksctl create cluster --name k8s --region ap-south-1 --version 1.35 --nodegroup-name k8s-nodes --node-type c7i-flex.large --nodes 1
```
### Log In Into EKS cluster
```sh
aws eks update-kubeconfig --name k8s
```
### `Delete EKS Cluster`
```sh
eksctl delete cluster --name k8s --region ap-south-1
```
### Install NGINX Ingress Controller (Manifests)
#### Apply the official manifest:
```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```
#### Verify installation:
```sh
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx
```
---
### Write `App1.yaml` file (Deployment + Service)
```sh
nano app1-deploy.yaml
```
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app1
  template:
    metadata:
      labels:
        app: app1
    spec:
      containers:
      - name: app1
        image: hashicorp/http-echo
        args:
        - "-text=Hello from App1"
 ports:
        - containerPort: 5678
---
apiVersion: v1
kind: Service
metadata:
  name: app1-svc
spec:
  selector:
    app: app1
  ports:
  - port: 80
    targetPort: 5678
```
```sh
kubectl apply -f app1-deploy.yaml
```
```sh
kubectl get svc
```
```sh
kubectl get pods -o wide
```

### Write `App2.yaml` file (Deployment + Service)
```sh
nano app2-deploy.yaml
```
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app2
spec:
  replicas: 1
selector:
    matchLabels:
      app: app2
  template:
    metadata:
      labels:
        app: app2
    spec:
      containers:
      - name: app2
        image: hashicorp/http-echo
        args:
        - "-text=Hello from App2"
        ports:
        - containerPort: 5678
---
apiVersion: v1
kind: Service
metadata:
  name: app2-svc
spec:
  selector:
    app: app2
  ports:
  - port: 80
    targetPort: 5678
```
```sh
kubectl apply -f app2-deploy.yaml
```
```sh
kubectl get svc
```
```sh
kubectl get pods -o wide
```
###  Write `Ingress.yaml` 
```sh
nano ingress.yaml
```
 - ####  Ex. Path-based Routing
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: path-based-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-svc
            port:
              number: 80
      - path: /app2
        pathType: Prefix
        backend:
          service:
            name: app2-svc
            port:
              number: 80
```
 - ####  Ex. Host/Name-based Routing
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: host-based-ingress
spec:
  ingressClassName: nginx
  rules:
  - host: app1.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: app1-svc
            port:
              number: 80
  - host: app2.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: app2-svc
            port:
              number: 80
```
---
