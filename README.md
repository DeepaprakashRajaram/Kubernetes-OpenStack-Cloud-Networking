# Kubernetes & OpenStack Cloud Networking Environment

![Kubernetes](https://img.shields.io/badge/Kubernetes-Cluster-blue)
![OpenStack](https://img.shields.io/badge/OpenStack-Cloud-orange)
![Linux](https://img.shields.io/badge/Linux-Ubuntu-yellow)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Overview

A practical implementation of a private cloud networking environment using **Kubernetes container orchestration** and **OpenStack cloud infrastructure**.

This project demonstrates the deployment and management of modern cloud networking concepts including virtualization, distributed systems, container networking, service discovery, application scaling, and load-balanced deployments.

The implementation includes:

- Multi-node Kubernetes cluster deployment using kubeadm
- Container orchestration using Kubernetes
- Container runtime configuration using containerd
- Pod networking using Flannel CNI
- Application deployment using Kubernetes Deployments
- Service exposure using NodePort
- Horizontal scaling and load balancing
- Private cloud infrastructure concepts using OpenStack


---

# Architecture

```
                    Host Machine
                         |
                  Oracle VirtualBox
                         |
        ---------------------------------
        |                               |
        |                               |
   OpenStack Cloud              Kubernetes Cluster

        |                               |

   Horizon Dashboard              Master Node
        |                              |
   Keystone Identity          kube-apiserver
        |                              |
 -----------------            -----------------
 |               |            |               |
Nova          Neutron      Scheduler        etcd
Compute       Network      Controller

        |                              |

 Virtual Machines              Worker Node
                                      |
                                  kubelet
                                      |
                                  containerd
                                      |
                          -----------------------
                          |          |          |
                        Pod 1      Pod 2      Pod 3
```


---

# Technologies Used

| Technology | Purpose |
|-|-|
| Ubuntu Linux | Operating System |
| VirtualBox | Virtualization Platform |
| Kubernetes | Container Orchestration |
| kubeadm | Cluster Deployment |
| containerd | Container Runtime |
| Flannel CNI | Kubernetes Networking |
| OpenStack | Private Cloud Platform |
| Horizon | OpenStack Dashboard |


---

# Kubernetes Implementation

A two-node Kubernetes cluster was created.

## Cluster Nodes

```
Master Node
192.168.56.20

Worker Node
192.168.56.21
```


## Control Plane Components

The master node manages the Kubernetes cluster.

Components:

- kube-apiserver
- kube-scheduler
- kube-controller-manager
- etcd


## Worker Node Components

The worker node executes application workloads.

Components:

- kubelet
- containerd
- Application Pods


---

# Cluster Verification

Command:

```bash
kubectl get nodes
```


Output:

```
NAME           STATUS      ROLES            VERSION

okd-master     Ready       control-plane    v1.29.15

okd-worker     Ready       worker           v1.29.15
```


Successfully created a functional Kubernetes cluster.


---

# Kubernetes Networking

The cluster uses **Flannel CNI** to provide overlay networking.

Implemented:

- Pod IP allocation
- Pod-to-Pod communication
- Cross-node networking
- Service discovery


Network:

```
Physical Network

Master Node
192.168.56.20


Worker Node
192.168.56.21



Flannel Overlay Network

10.244.0.0/16


Example Pods:

nginx-pod-1 : 10.244.1.2

nginx-pod-2 : 10.244.1.3

nginx-pod-3 : 10.244.1.4
```


---

# Application Deployment

A containerized Nginx web application was deployed.

Create deployment:

```bash
kubectl create deployment nginx --image=nginx
```


Verify pods:

```bash
kubectl get pods -o wide
```


---

# Service Exposure

The application was exposed externally using NodePort.

Command:

```bash
kubectl expose deployment nginx \
--type=NodePort \
--port=80
```


Service:

```
User

 |
 |
 
NodePort Service

 |
 |

nginx Pods
```


Example access:

```
http://192.168.56.21:30896
```


---

# Load Balancing Demonstration

The deployment was scaled to multiple replicas.

Command:

```bash
kubectl scale deployment nginx --replicas=3
```


Architecture:

```

               Client

                  |

          Kubernetes Service

                  |

       -----------------------

       |          |          |

    Pod 1      Pod 2      Pod 3

```


Kubernetes automatically distributes requests across available pods.


---

# OpenStack Implementation

OpenStack was configured to demonstrate private cloud infrastructure management.

Implemented services:


| Component | Function |
|-|-|
| Nova | Virtual Machine Management |
| Neutron | Cloud Networking |
| Keystone | Authentication and Authorization |
| Glance | Image Management |
| Horizon | Web Dashboard |


---

# OpenStack Architecture

```

User

 |

Horizon Dashboard

 |

Keystone Authentication

 |

--------------------------------

|              |               |

Nova        Neutron        Glance

 |

Virtual Machines

```


---

# Troubleshooting Experience

During implementation, several real-world Kubernetes issues were identified and solved.

Examples:

### Container Runtime Issue

Problem:

```
unknown service runtime.v1.RuntimeService
```

Solution:

- Fixed containerd CRI configuration
- Enabled SystemdCgroup
- Restarted container runtime


### Node NotReady Issue

Cause:

- Missing CNI networking plugin

Solution:

- Installed Flannel CNI


### Worker Join Failure

Cause:

- Expired bootstrap token

Solution:

Generated new join command:

```bash
kubeadm token create --print-join-command
```


---

# Concepts Demonstrated

- Cloud Computing
- Infrastructure as a Service (IaaS)
- Virtualization
- Container Orchestration
- Distributed Networking
- Overlay Networks
- Container Network Interface (CNI)
- Service Discovery
- Load Balancing
- Kubernetes Cluster Administration
- Cloud Resource Management


---

# Future Enhancements

- Add Prometheus and Grafana monitoring
- Implement Kubernetes Ingress Controller
- Configure persistent storage
- Automate deployment using Ansible
- Add CI/CD pipeline integration
- Expand Kubernetes cluster with additional worker nodes


---

# Result

Successfully designed and implemented a private cloud and container orchestration environment using **OpenStack and Kubernetes**, demonstrating modern cloud networking principles used in real-world cloud infrastructure.
