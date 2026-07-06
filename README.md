# Kubernetes-OpenStack-Cloud-Networking
Implementation of a private cloud networking environment using Kubernetes and OpenStack with multi-node clusters, container networking, service discovery, and load-balanced deployments.

# Kubernetes & OpenStack Cloud Networking Environment

## Project Overview

This project demonstrates the design and implementation of a private cloud networking environment using Kubernetes and OpenStack.

The objective of this project is to understand modern cloud infrastructure concepts including virtualization, container orchestration, cluster networking, service discovery, and application deployment in a distributed environment.

The implementation consists of:
- A multi-node Kubernetes cluster using kubeadm
- Container networking using Flannel CNI
- Application deployment using Kubernetes Deployments
- Service exposure using NodePort
- Pod scaling and load balancing
- Private cloud management using OpenStack


---

# Architecture

```
                    Host Machine
                         |
                    VirtualBox
                         |
        ---------------------------------
        |                               |
   OpenStack Cloud              Kubernetes Cluster
        |                               |
  ----------------              -----------------
  | Controller |                | Master Node    |
  | Compute    |                | API Server     |
  ----------------              | Scheduler      |
                                | Controller     |
                                | etcd           |
                                -----------------
                                       |
                                -----------------
                                | Worker Node    |
                                | kubelet        |
                                | containerd     |
                                | Pods           |
                                -----------------
```


---

# Technologies Used

- Ubuntu Linux
- Oracle VirtualBox
- Kubernetes
- kubeadm
- containerd
- Flannel CNI
- OpenStack
- Horizon Dashboard


---

# Kubernetes Implementation

A two-node Kubernetes cluster was configured.

## Master Node

Responsible for managing the cluster:

- kube-apiserver
- kube-scheduler
- kube-controller-manager
- etcd


## Worker Node

Responsible for running application workloads:

- kubelet
- container runtime
- application pods


Cluster verification:

```bash
kubectl get nodes
```

Output:

```
NAME          STATUS    ROLES            VERSION

okd-master    Ready     control-plane    v1.29.15
okd-worker    Ready     <none>           v1.29.15
```


---

# Kubernetes Networking

The cluster uses Flannel CNI for pod networking.

Features demonstrated:

- Pod-to-Pod communication
- Internal Cluster Networking
- Service Discovery
- NodePort Access


---

# Application Deployment

Nginx container application was deployed:

```bash
kubectl create deployment nginx --image=nginx
```

Service exposed:

```bash
kubectl expose deployment nginx \
--type=NodePort \
--port=80
```

Deployment scaled:

```bash
kubectl scale deployment nginx --replicas=3
```


Result:

```
nginx pod 1 ----|
nginx pod 2 ----|---- Kubernetes Service ---- Client
nginx pod 3 ----|
```


---

# Load Balancing

Multiple replicas of the application were created.

Kubernetes Service automatically distributes traffic between available pods.


---

# OpenStack Implementation

OpenStack was configured to provide private cloud infrastructure.

Main components:

| Component | Purpose |
|-|-|
| Nova | Virtual machine management |
| Neutron | Cloud networking |
| Keystone | Authentication |
| Glance | Image management |
| Horizon | Web dashboard |


---

# Concepts Demonstrated

- Cloud Computing
- Infrastructure Virtualization
- Container Orchestration
- Distributed Networking
- Overlay Networks
- Service Discovery
- Load Balancing


---

# Result

Successfully created a private cloud and container orchestration environment demonstrating real-world cloud networking principles using Kubernetes and OpenStack.
