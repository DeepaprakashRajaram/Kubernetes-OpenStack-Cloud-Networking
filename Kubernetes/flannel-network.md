# Kubernetes Networking using Flannel CNI

## Overview

This document explains the networking implementation used in the Kubernetes cluster.

Kubernetes requires a Container Network Interface (CNI) plugin to enable communication between pods across different nodes.

This project uses Flannel CNI to create an overlay network between Kubernetes nodes.


---

# Why CNI is Required

By default, containers running on different nodes cannot communicate directly.

A CNI plugin provides:

- Pod IP allocation
- Inter-node communication
- Routing between containers
- Overlay networking


---

# Flannel CNI

Flannel is a lightweight Kubernetes networking solution.

It creates a virtual network layer above the physical network.

Physical Network:

```
Master Node
192.168.56.20


Worker Node
192.168.56.21
```


Flannel Overlay Network:

```
Pod Network

10.244.0.0/16


Example:

nginx-pod-1
10.244.1.2


nginx-pod-2
10.244.1.3


nginx-pod-3
10.244.1.4
```


---

# Network Architecture


```

                Kubernetes Cluster


            +----------------+
            | Master Node    |
            |                |
            | API Server     |
            +----------------+
                    |
                    |
              Flannel VXLAN
              Overlay Network
                    |
                    |
            +----------------+
            | Worker Node    |
            |                |
            | Pod 1          |
            | Pod 2          |
            | Pod 3          |
            +----------------+


```


---

# Pod-to-Pod Communication


Example:

Pod A:

```
10.244.1.2
```


communicates with:

Pod B:

```
10.244.1.3
```


without NAT.


Test:

```bash
kubectl exec -it <pod-name> -- ping <pod-ip>
```


---

# Kubernetes Service Networking


Pods are temporary and IP addresses can change.

Services provide a permanent access point.


Example:

```
Client

  |

NodePort Service

  |

Load Balancer

  |

Pods
```


---

# NodePort Access


Service:

```bash
kubectl get svc
```


Example:

```
nginx NodePort 80:30896
```


Access:

```
http://192.168.56.21:30896
```


Traffic reaches the worker node and is forwarded to available nginx pods.


---

# Concepts Demonstrated

- Container Network Interface (CNI)
- Overlay Networking
- VXLAN
- Pod IP Addressing
- Service Networking
- Kubernetes Load Balancing
