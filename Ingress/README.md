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
## Notes 
### Ingress rule
 - This object ensures or rather its a rule book which states that which a user what to view a particular microservicce the traffic will diverted to that particular microservice cluster IP service object
### Ingress controller
 - Ensure that the traffic requested by the user has requested the desired destination it will route the trafic to desired destination.
---
<img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/a817af63-7f38-4ff0-b7df-1a306096f14a" />

---
