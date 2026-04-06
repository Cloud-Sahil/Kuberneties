# Kubernetes Pods and Services
---
## Introduction to Pods and Services
### Pods
A Pod is the smallest deployable unit in Kubernetes, encapsulating one or more containers with shared resources like storage and network.

- **Lifecycle**:
  - Pending → Running → Succeeded/Failed → Terminated

- **Use Cases**:
  - Running a single application container.
  - Running multiple containers that share resources and are tightly coupled (e.g., sidecar patterns).

### Services
Services provide stable networking and expose Pods to other applications or external traffic.

- **Types of Services**:
  1. **ClusterIP**: Exposes the service within the cluster.
  2. **NodePort**: Exposes the service on each node’s IP at a static port.
  3. **LoadBalancer**: Exposes the service to the internet using a cloud provider’s load balancer.

| Service Type     | Accessible From         | Typical Use Case                                | Example Access URL            |
| ---------------- | ----------------------- | ----------------------------------------------- | ----------------------------- |
| **ClusterIP**    | Inside cluster only     | Microservice-to-microservice communication      | `http://backend-service:8080` |
| **NodePort**     | External (via node IP)  | Testing or small setups without a load balancer | `http://<node-ip>:30080`      |
| **LoadBalancer** | Internet (via cloud LB) | Production applications accessible publicly     | `http://<public-ip>`          |

#### ClusterIP (Internal Access Only)
#### NodePort (Access from Browser using Node IP)
#### LoadBalancer (Public IP – Cloud Only)
---
## Kubernetes Networking: Intra-Pod and Inter-Pod Communication

Kubernetes networking is fundamental for ensuring smooth communication between various components, including pods, services, and external clients. It provides flexible networking configurations for intra-pod and inter-pod communication.

### Intra-Pod Communication
- **Definition**: Intra-pod communication refers to the communication between containers within the same pod.
- **Mechanism**: Containers in a pod share the same network namespace, which means they:
  - Share the same IP address.
  - Can communicate directly using `localhost` and exposed container ports.

### Inter-Pod Communication
- **Definition**: Inter-pod communication refers to the communication between pods.
- **Mechanism**:
  - Kubernetes assigns each pod a unique IP address.
  - Pods communicate directly using these IP addresses or via Kubernetes services.
  - Kubernetes ensures a flat network model where all pods can communicate without NAT.
---
