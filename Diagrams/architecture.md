# Cloud Infrastructure Architecture

## Project Architecture

This project combines Kubernetes container orchestration with OpenStack private cloud infrastructure.

---

# Overall Architecture


```
                 User / Client
                       |
                       |
                Web Interface
                       |
        --------------------------------
        |                              |
        |                              |
   OpenStack Cloud              Kubernetes Cluster

        |                              |

   Horizon Dashboard              Master Node
        |                              |
   Keystone Auth              Kubernetes API Server
        |                              |
   ----------------          ----------------------
   |              |          |                    |
 Nova          Neutron    Scheduler           etcd
Compute       Network       


        |                              |

 Virtual Machines              Worker Node
                                      |
                                      |
                                  containerd
                                      |
                                      |
                          -----------------------
                          |          |          |
                       Pod 1      Pod 2      Pod 3

```

---

# Kubernetes Network Architecture


```

External User

      |

 NodePort Service

      |

 Kubernetes Service

      |

 Load Balancer

      |

 -----------------

 |       |       |

Pod1   Pod2   Pod3


```


---

# Kubernetes Node Communication


```

Master Node
192.168.56.20

       |
       |
 Flannel Overlay Network
       |
       |

Worker Node
192.168.56.21

       |

Application Pods

10.244.1.x


```

---

# Network Flow

1. User sends request

2. NodePort receives traffic

3. Kubernetes Service forwards request

4. Traffic reaches available pod

5. Response returned to user


---

# Concepts Represented

- Cloud Architecture
- Cluster Networking
- Container Networking
- Virtualization
- Service Discovery
- Load Balancing
