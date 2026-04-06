# Kuberneties (K8S)
---
## Introduction to Kubernetes

- **Kubernetes (K8s)** is an open-source **container orchestration platform** used to automate the deployment, scaling, and management of containerized applications.
- It was originally developed by **Google** and is now maintained by the **Cloud Native Computing Foundation (CNCF)**.
- Kubernetes manages containers (typically Docker containers) across a group of machines called a **cluster**.
- It ensures applications run **reliably, scalable, and self-healing**.

### Key Features

- Automated deployment
- Auto scaling
- Load balancing
- Self-healing (restart failed containers)
- Rolling updates and rollbacks
- Service discovery

---
## Why We Need an Orchestration Tool

When applications run using **many containers**, managing them manually becomes difficult.

### Problems Without Orchestration

- Difficult to manage **multiple containers**
- Manual **scaling**
- No automatic **load balancing**
- No **automatic recovery**
- Complex **container networking**

### Role of Orchestration Tools

Container orchestration tools automate:

| Feature | Description |
|-------|-------------|
| Deployment | Automatically deploy containers |
| Scaling | Increase or decrease containers based on load |
| Load Balancing | Distribute traffic across containers |
| Self Healing | Restart failed containers |
| Resource Management | Efficient CPU and memory usage |

### Examples of Orchestration Tools

- Kubernetes
- Docker Swarm
- Apache Mesos

---
## Why Kubernetes?
Kubernetes has emerged as the preferred orchestration tool for several reasons:
1. **Open Source**: Vendor-neutral and community-driven.
2. **Scalability**: Designed to handle large-scale workloads.
3. **Portability**: Works across on-premises, cloud, and hybrid environments.
4. **Extensibility**: Highly customizable through APIs and plugins.
5. **Resilience**: Automatic healing of failed containers and rescheduling.
6. **Comprehensive Ecosystem**: Supported by a wide range of tools and platforms.
---
## Architecture of Kubernetes


<img width="1536" height="1024" alt="Kubernetes architecture overview and components" src="https://github.com/user-attachments/assets/0e68cf54-4aff-4d56-8a86-712dc1bc569d" />

---
## Control Plane (Master Node)                              |               ## Worker Node

The control plane manages the entire cluster.               |               Worker nodes run the application containers.

| Component | Role |                                        |               | Component | Role |
|----------|------|                                                        |----------|------|
| API Server | Entry point for all cluster communication |       |          | Kubelet | Communicates with control plane |
| Scheduler | Assigns pods to worker nodes |                     |          | Container Runtime | Runs containers (Docker / containerd) |
| Controller Manager | Maintains desired cluster state |         |          | Kube Proxy | Handles networking and load balancing |
| etcd | Key-value database storing cluster data |               |          | Pods | Smallest deployable unit in Kubernetes |


---
## Worker Node

Worker nodes run the application containers.

| Component | Role |
|----------|------|
| Kubelet | Communicates with control plane |
| Container Runtime | Runs containers (Docker / containerd) |
| Kube Proxy | Handles networking and load balancing |
| Pods | Smallest deployable unit in Kubernetes |

---
