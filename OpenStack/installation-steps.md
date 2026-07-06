# OpenStack Installation and Configuration

## Overview

This document explains the setup process followed to create a private cloud environment using OpenStack.

The implementation demonstrates cloud infrastructure deployment, virtualization, networking, and resource management.

---

# Environment

Virtualization Platform:

```
Oracle VirtualBox
```

Operating System:

```
Ubuntu Linux
```

Deployment:

```
OpenStack Controller Node
OpenStack Compute Services
```

---

# System Preparation

Update system packages:

```bash
sudo apt update
sudo apt upgrade -y
```

Install required dependencies:

```bash
sudo apt install software-properties-common -y
```

---

# OpenStack Installation

OpenStack services were installed and configured to create a private cloud environment.

Core services:

- Keystone
- Nova
- Neutron
- Glance
- Horizon

---

# Horizon Dashboard

The OpenStack dashboard provides web-based cloud management.

Access:

```
http://controller-ip/dashboard
```

Example:

```
http://192.168.56.20/dashboard
```

Login:

```
Domain: Default

Username: admin

Password: configured admin password
```

---

# Instance Management

Virtual machines can be launched from Horizon.

Steps:

1. Open Horizon Dashboard

2. Navigate:

```
Compute → Instances
```

3. Select:

```
Launch Instance
```

4. Configure:

- Instance name
- Image
- Flavor
- Network

5. Start instance


---

# Networking Configuration

Managed using Neutron.

Configured:

- Virtual networks
- Subnets
- Routers
- Floating IP addressing


Network flow:

```

VM Instance

     |

Virtual Network

     |

Router

     |

External Network


```

---

# Image Management

Glance stores operating system images.

Images are used as templates for VM creation.


Example:

```
Ubuntu Image

      |

Glance

      |

Nova

      |

Virtual Machine
```

---

# Verification

Check OpenStack services:

```bash
openstack service list
```

Check instances:

```bash
openstack server list
```

Check networks:

```bash
openstack network list
```


---

# Concepts Demonstrated

- Private Cloud Deployment
- Virtual Machine Provisioning
- Virtual Networking
- Cloud Authentication
- Infrastructure Management

---

# Result

A functional private cloud environment was created using OpenStack services.
