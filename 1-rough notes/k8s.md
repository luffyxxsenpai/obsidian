# k8s architecture
---
Date: 22,Oct,2024
subject: 
field: [[devops]] [[k8s]]
tags:

---
# architecture 

![[Pasted image 20241022172836.jpg]]

### **Control Plane**

The control plane manages the overall Kubernetes cluster. It makes decisions about scheduling, scaling, and responding to cluster events. The control plane components include the API server, scheduler, controller manager, etcd, and optionally, the cloud controller manager. The control plane runs on the master nodes and controls the worker nodes.
### **API (Kubernetes API Server)**

The **API server** is the central hub for all interactions within the Kubernetes cluster. It exposes the Kubernetes API and serves as the front-end for the control plane. All communication between internal components, external users, and administrators happens through the API server.
### **Node**

A **node** is a physical or virtual machine that runs as part of a Kubernetes cluster. It is responsible for running the containerized applications. Each node contains the necessary services to be managed by the control plane, such as the container runtime, `kubelet`, and `kube-proxy`. Nodes can be categorized into **worker nodes** (which run workloads) and **master nodes** (which run control plane components).
### **Container Runtime**

The **container runtime** is the software responsible for running containers on a node. Kubernetes supports multiple container runtimes, such as Docker, containerd, or CRI-O. The container runtime is responsible for pulling container images, starting, and stopping containers.
### **Kube Proxy**

The **kube-proxy** is a network component that runs on each node in the cluster. It maintains network rules and routes traffic between services and pods. It ensures that the networking layer within Kubernetes is abstracted, allowing communication between different pods, services, and external networks.

### **Kubelet**

The **kubelet** is an agent that runs on each node and ensures that containers are running in pods as expected. It communicates with the control plane components (especially the API server) and receives the desired pod state (e.g., what containers should be running). The kubelet ensures that the actual state of the node matches the desired state.
### **Scheduler**

The **scheduler** is a control plane component responsible for assigning pods to specific nodes in the cluster. It determines the best node for a pod to run on based on resource requirements, constraints, and current workloads. The scheduler ensures efficient resource utilization and availability across the cluster.
### **Controller Manager**

The **controller manager** runs a collection of controllers that handle routine tasks within Kubernetes. Each controller is responsible for regulating the state of the system (e.g., ensuring that the number of replicas of an application matches the desired state). Examples include the replication controller, node controller, and job controller.
### **Cloud Controller Manager**

The **cloud controller manager** integrates Kubernetes with cloud service providers (e.g., AWS, Azure, GCP). It handles cloud-specific control logic, such as managing load balancers, handling storage, and interacting with the underlying cloud infrastructure. It abstracts away the differences between different cloud platforms.
### **etcd Database**

**etcd** is a highly available, distributed key-value store that stores all the cluster data. It serves as Kubernetes' backing store, saving the configuration data, state, and metadata of the entire cluster. All the objects and configurations in Kubernetes, such as nodes, pods, services, and deployments, are stored in etcd.

---

### namespace
- provides a mechanism to group resources within a cluster
- default namespaces are *default, kube-system, kube-node-lease, kube-public*
-   

![[Pasted image 20241023211025.png]]