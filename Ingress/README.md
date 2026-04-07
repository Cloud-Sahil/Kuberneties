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





### Sample Applications
✅ App1 (Deployment + Service)
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
### ✅ App2 (Deployment + Service)
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
### Ingress Examples
**✅ Path-based Routing**
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
**✅ Host/Name-based Routing**
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
