# OpenStack Cloud Infrastructure Components

## Overview

OpenStack is an open-source cloud computing platform used to build and manage private and public cloud environments.

It provides Infrastructure as a Service (IaaS), allowing users to create and manage:

- Virtual machines
- Networks
- Storage
- Images
- Users and projects


---

# OpenStack Architecture

```

                User

                 |
                 |

          Horizon Dashboard

                 |
                 |

            Keystone
        Authentication

                 |

--------------------------------

|              |               |

Nova        Neutron        Glance

Compute     Network        Images

|


Virtual Machines


```


---

# Components Implemented


## 1. Horizon Dashboard

Horizon provides the web-based graphical interface for OpenStack.

It allows users to:

- Manage instances
- Configure networks
- Manage images
- Monitor resources


---

## 2. Keystone (Identity Service)

Keystone provides authentication and authorization.

Responsibilities:

- User authentication
- Role management
- Token generation
- Service access control


Example:

```
User Login
     |
Keystone Verification
     |
Access OpenStack Services
```


---

## 3. Nova (Compute Service)

Nova manages virtual machine instances.

Responsibilities:

- Creating VMs
- Scheduling workloads
- Managing compute nodes


Workflow:

```
User Request

      |

Nova Scheduler

      |

Compute Node

      |

Virtual Machine
```


---

## 4. Neutron (Networking Service)

Neutron provides cloud networking.

Features:

- Virtual networks
- Subnets
- Routers
- IP address management


Example:

```
Virtual Machine

       |

Virtual Network

       |

Router

       |

External Network
```


---

## 5. Glance (Image Service)

Glance stores and manages operating system images.

Examples:

- Ubuntu image
- Cirros image
- Custom VM images


Nova uses Glance images to launch instances.


---

# Controller Node

The controller node manages:

- Authentication services
- APIs
- Scheduling
- Dashboard


---

# Compute Node

The compute node provides:

- CPU resources
- Memory resources
- Virtual machine execution


---

# Concepts Demonstrated

- Cloud Computing
- Infrastructure as a Service (IaaS)
- Virtualization
- Software Defined Networking
- Cloud Resource Management
