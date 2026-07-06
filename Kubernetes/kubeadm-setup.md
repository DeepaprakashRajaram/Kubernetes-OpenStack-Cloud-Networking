# Kubernetes Cluster Setup using kubeadm

## Overview

This document explains the setup process for creating a multi-node Kubernetes cluster using kubeadm.

The cluster contains:

- 1 Control Plane Node
- 1 Worker Node

Environment:

- Virtualization: Oracle VirtualBox
- Operating System: Ubuntu Server
- Container Runtime: containerd
- Kubernetes Version: v1.29.15


---

# Cluster Architecture

```
             Kubernetes Cluster


              Master Node
          (Control Plane)

        kube-apiserver
        kube-scheduler
        controller-manager
        etcd

                |
                |
          Flannel Network

                |
                |

             Worker Node

             kubelet
             containerd
             nginx pods
```


---

# System Preparation

Disable swap:

```bash
sudo swapoff -a
```

Enable required kernel modules:

```bash
sudo modprobe overlay
sudo modprobe br_netfilter
```


Configure networking:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```


---

# Container Runtime Configuration

containerd was used as the Kubernetes container runtime.

Restart containerd:

```bash
sudo systemctl restart containerd
```

Verify:

```bash
sudo systemctl status containerd
```


---

# Initialize Master Node

The Kubernetes control plane was initialized using:

```bash
sudo kubeadm init \
--apiserver-advertise-address=192.168.56.20 \
--pod-network-cidr=10.244.0.0/16
```


---

# Configure kubectl Access


```bash
mkdir -p $HOME/.kube
```

Copy admin configuration:

```bash
sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config
```

Change ownership:

```bash
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```


Verify:

```bash
kubectl get nodes
```


---

# Install Flannel CNI

Flannel was installed for Kubernetes pod networking.

```bash
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
```


---

# Join Worker Node

A worker node was connected using:

```bash
sudo kubeadm join <MASTER-IP>:6443 \
--token <TOKEN> \
--discovery-token-ca-cert-hash <HASH>
```


---

# Final Cluster Status


```bash
kubectl get nodes
```


Output:


```
NAME          STATUS     ROLES

okd-master    Ready      control-plane

okd-worker    Ready      worker
```


The Kubernetes cluster was successfully created.
