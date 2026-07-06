# Kubernetes Application Deployment and Networking Demo

## Overview

This document demonstrates deploying a containerized application inside the Kubernetes cluster.

The demo includes:

- Creating a deployment
- Running application pods
- Exposing applications using services
- Scaling replicas
- Load balancing
- Pod networking verification


---

# Deploy Nginx Application

A sample Nginx web server was deployed.

Command:

```bash
kubectl create deployment nginx --image=nginx
```

Verify deployment:

```bash
kubectl get deployments
```


---

# Check Running Pods

Command:

```bash
kubectl get pods -o wide
```

Example output:

```
NAME                    READY     STATUS      IP

nginx-xxxxx             1/1       Running     10.244.1.2
```

The pod was scheduled on the worker node.


---

# Expose Application Using NodePort

The deployment was exposed externally using Kubernetes Service.

Command:

```bash
kubectl expose deployment nginx \
--type=NodePort \
--port=80
```


Check service:

```bash
kubectl get svc
```


Example:

```
NAME      TYPE        PORT

nginx     NodePort    80:30896/TCP
```


The application can now be accessed using:

```
http://worker-node-ip:nodeport
```


Example:

```
http://192.168.56.21:30896
```


---

# Scaling Application

The deployment was scaled to multiple replicas.

Command:

```bash
kubectl scale deployment nginx --replicas=3
```


Verify:

```bash
kubectl get pods -o wide
```


Output:

```
nginx-pod-1     Running
nginx-pod-2     Running
nginx-pod-3     Running
```


---

# Load Balancing

Traffic flow:

```
              Client

                 |
                 |

          Kubernetes Service

        /        |        \

     Pod 1     Pod 2     Pod 3
```


Kubernetes automatically distributes traffic between available pods.


---

# Pod Communication Test

Enter a pod:

```bash
kubectl exec -it <pod-name> -- bash
```


Ping another pod:

```bash
ping <pod-ip>
```


This verifies internal Kubernetes networking.


---

# Concepts Demonstrated

- Container orchestration
- Cluster networking
- NodePort service exposure
- Horizontal scaling
- Load balancing
- Service discovery
