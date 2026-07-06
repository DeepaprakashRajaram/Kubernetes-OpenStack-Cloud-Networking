# Kubernetes Troubleshooting Notes

## Overview

During the implementation of the Kubernetes cluster, several real-world configuration issues were identified and resolved.

This document records common problems and their solutions.


---

# 1. Container Runtime Issue

## Problem

During kubeadm initialization:

```
container runtime is not running

unknown service runtime.v1.RuntimeService
```


## Cause

containerd CRI plugin configuration issue.


## Solution

Configured containerd:

```toml
version = 2

[plugins."io.containerd.grpc.v1.cri"]

[plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]

SystemdCgroup = true
```


Restarted services:

```bash
sudo systemctl restart containerd
sudo systemctl restart kubelet
```


---

# 2. Kubernetes API Connection Refused


## Problem

```
connection refused localhost:8080
```


## Cause

kubectl configuration missing.


## Solution


Configured kubeconfig:


```bash
mkdir -p $HOME/.kube

sudo cp /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
```


---

# 3. Node Showing NotReady


## Problem

```
okd-master NotReady
```


## Cause

CNI plugin was missing.


## Solution

Installed Flannel:


```bash
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
```


---

# 4. Worker Node Join Issue


## Problem


```
bootstrap token invalid
```


## Solution


Generated a new token:


```bash
kubeadm token create --print-join-command
```


Used the new join command on worker node.


---

# 5. Verification Commands


Check nodes:


```bash
kubectl get nodes
```


Check pods:


```bash
kubectl get pods -A
```


Check services:


```bash
kubectl get svc
```


---

# Result


All issues were resolved and a stable Kubernetes cluster was created.
