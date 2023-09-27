---
title: "🗬 Important Kubernetes interview questions 📜"
seoTitle: "🗬 Important Kubernetes interview questions 📜"
datePublished: Wed Sep 27 2023 02:35:43 GMT+0000 (Coordinated Universal Time)
cuid: cln14wkbs000009m9he5e7jqd
slug: important-kubernetes-interview-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695609614882/1b3284c8-6b1d-404b-9e49-0c48034c2bdd.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1695609640229/7e1fe3b5-7a51-427e-8348-ec3b2f6d975e.png
tags: interview, kubernetes, devops, 90daysofdevops, trainwithshubham

---

## 📍 Introduction

### 🔸 What is Kubernetes and why it is important?

Kubernetes is an open-source container orchestration platform developed by Google. It is used for automating the deployment, scaling, and management of containerized applications. Kubernetes is important because it provides several benefits:

* **Scalability:** Kubernetes allows you to easily scale applications up or down to meet changing demands.
    
* **High Availability:** It ensures that applications remain available and resilient even when individual components fail.
    
* **Resource Optimization:** Kubernetes optimizes resource allocation, ensuring efficient utilization of computing resources.
    
* **Declarative Configuration:** You can define your application's desired state, and Kubernetes will work to maintain that state, making it easier to manage complex applications.
    
* **Portability:** Kubernetes provides a consistent platform for deploying and managing applications across various cloud providers and on-premises environments.
    

### 🔸 What is the difference between docker swarm and Kubernetes?

Docker Swarm and Kubernetes are both container orchestration solutions, but they have several differences:

* **Orchestration Philosophy:** Kubernetes is a powerful, complicated system for managing big container setups and complex apps. Docker Swarm is simpler and easy to start, great for smaller projects.
    
* **Ecosystem:** Kubernetes has a larger ecosystem with a wide range of third-party tools and extensions, whereas Docker Swarm is more tightly integrated with Docker.
    
* **Configuration:** Kubernetes uses YAML or JSON files for configuration, while Docker Swarm uses simple CLI commands.
    
* **Scaling:** Kubernetes offers more advanced scaling options, including auto-scaling based on resource utilization, whereas Docker Swarm provides basic scaling features.
    
* **Networking:** Kubernetes offers more advanced networking capabilities and supports various network plugins, whereas Docker Swarm has simpler networking options.
    

### 🔸How does Kubernetes handle network communication between containers?

Kubernetes employs a combination of network namespaces, IP address allocation, and a Container Network Interface (CNI) plugin to facilitate network communication among containers.

Each pod in Kubernetes has its IP address, and containers within the same pod can communicate with each other using localhost. Containers in different pods can communicate through the pod's IP address and port mapping. CNI plugins enable the configuration of advanced network policies and connectivity options.

### 🔸 How does Kubernetes handle the scaling of applications?

Kubernetes provides two primary mechanisms for scaling applications:

* **Horizontal Pod Autoscaling (HPA):** This feature automatically modifies the number of pod replicas according to resource utilization metrics (e.g., CPU or memory usage) or user-defined custom metrics. It ensures that your application scales in or out to accommodate demand.
    
* **Manual Scaling:** You can manually scale your application by adjusting the desired number of replicas in a Deployment or ReplicaSet configuration. This approach provides you with greater control over the scaling process.
    

### 🔸 What is a Kubernetes Deployment and how does it differ from a ReplicaSet?

A Kubernetes Deployment is a higher-level resource used to declaratively manage the deployment and scaling of pods. It provides the following features that differentiate it from a ReplicaSet:

* **Declarative Updates:** Deployments allow you to specify the desired state of your application, and Kubernetes takes care of achieving and maintaining that state. You can easily roll out updates and rollbacks.
    
* **Rolling Updates:** Deployments facilitate rolling updates by gradually replacing old pods with new ones, ensuring that the application remains available during the update process.
    
* **Versioning:** Deployments allow you to manage multiple versions of your application, making it easy to switch between different releases.
    

A ReplicaSet, on the other hand, is a lower-level resource that simply ensures a specified number of pod replicas are running. Deployments use ReplicaSets internally but add a layer of abstraction and additional functionality for managing application deployments.

### 🔸 Can you explain the concept of rolling updates in Kubernetes?

Rolling updates in Kubernetes are a strategy for updating an application with minimal downtime. Here's how it works:

1. A new version of your application is deployed alongside the existing version.
    
2. Kubernetes gradually replaces old pods with new ones, ensuring that the desired number of replicas is maintained throughout the update.
    
3. This gradual replacement minimizes downtime and allows you to monitor the new version's health before fully transitioning.
    

Rolling updates are typically managed using Kubernetes Deployments. You can define the new version of your application in a new pod template, and Kubernetes will automatically manage the update process, rolling out new pods while rolling in old ones.

### 🔸 How does Kubernetes handle network security and access control?

Kubernetes provides several mechanisms to manage network security and access control:

* **Network Policies:** Network Policies are used to define rules that control network traffic between pods. They allow you to specify which pods can communicate with each other based on labels and namespaces, effectively creating network segmentation.
    
* **RBAC (Role-Based Access Control):** RBAC allows you to define roles and role bindings that control access to resources within the Kubernetes cluster. You can grant or restrict permissions for users, service accounts, or groups.
    
* **Pod Security Policies:** These policies enforce security requirements on pods, such as restricting container capabilities, hostPath usage, and other security-related settings.
    
* **Service Accounts:** Service accounts are used to control the permissions and access tokens that pods have within the cluster, limiting what they can do and access.
    
* **TLS and Secrets:** Kubernetes supports secure communication through Transport Layer Security (TLS) certificates and secrets management, ensuring data confidentiality and integrity.
    

### 🔸 Can you give an example of how Kubernetes can be used to deploy a highly available application?

To deploy a highly available application in Kubernetes, you can follow these steps:

1. **ReplicaSets or Deployments:** Use ReplicaSets or Deployments to manage the desired number of pod replicas for your application. Ensure that you have multiple replicas running for each component of your application.
    
2. **Node Distribution:** Spread your pods across multiple nodes to minimize the risk of a single node failure affecting your entire application.
    
3. **Load Balancing:** Set up a load balancer service or use Ingress to distribute traffic evenly across the pods of your application. This ensures that traffic is routed to healthy pods and provides a level of fault tolerance.
    
4. **Health Checks:** Implement readiness and liveness probes to monitor the health of your application pods. Kubernetes will automatically replace or reschedule pods that fail these checks.
    
5. **Persistent Storage:** Use Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) to ensure that your application's data is stored persistently and can survive pod failures.
    
6. **Auto-Scaling:** If traffic fluctuates, configure Horizontal Pod Autoscaling (HPA) to automatically adjust the number of pod replicas based on resource usage, ensuring optimal performance.
    
7. **Monitoring and Alerts:** Set up monitoring and alerting tools like Prometheus and Grafana to keep an eye on the health and performance of your application and the Kubernetes cluster itself.
    

By following these practices, you can deploy a highly available application that can withstand node failures, hardware issues, and varying levels of traffic.

### 🔸 What is a namespace in Kubernetes? Which namespace does any pod take if we don't specify any namespace?

A namespace in Kubernetes is a logical partition within a physical cluster that organizes and isolates resources, applications, and objects; if not specified, a pod is created in the default namespace.

### 🔸 How does ingress help in Kubernetes?

* Ingress is a Kubernetes resource that plays a crucial role in managing external access to services within the cluster. It acts as a layer-7 HTTP/HTTPS reverse proxy and offers the following benefits:
    
* **HTTP Routing:** Ingress allows you to define rules and routing configurations based on HTTP attributes such as hostname, path, and headers. This enables you to route incoming traffic to specific services based on the request's characteristics.
    
* **Load Balancing:** Ingress controllers (like Nginx, Traefik, or HAProxy) can perform load balancing across multiple backend services, ensuring even distribution of traffic.
    
* **TLS Termination:** Ingress can handle SSL/TLS termination, enabling secure communication with your services. You can configure TLS certificates for encryption and decryption.
    
* **Path-Based Routing:** Ingress allows you to map specific paths (e.g., `/app1`, `/app2`) to different services, making it useful for hosting multiple applications behind a single load balancer.
    
* **Rewrites and Redirects:** Ingress controllers often support URL rewrites and redirects, helping you manage URL changes and routing adjustments.
    

In essence, Ingress simplifies the management of external access to services, especially in scenarios where you have multiple services running within your Kubernetes cluster and need to expose them to the internet or other internal networks.

### 🔸 Explain different types of services in Kubernetes.

Kubernetes provides various types of services to expose applications within the cluster:

* **ClusterIP:** This service type exposes a group of pods within the cluster through a stable internal IP. It enables other pods within the cluster to access the service using this IP. ClusterIP services are commonly utilized for internal communication between application components.
    
* **NodePort:** NodePort services expose a service on a fixed port on each node's IP address. This implies that the service can be accessed externally on each node's IP at the designated port. NodePort services are frequently employed in situations where external access to a service is required, but they might not be appropriate for production use without further configuration.
    
* **LoadBalancer:** LoadBalancer services integrate with cloud provider load balancers to distribute external traffic to the service. They are suitable for exposing services to the internet or external networks. The cloud provider provisions and configures the load balancer, distributing traffic to the service's pods.
    
* **ExternalName:** ExternalName services provide a DNS-based mapping to an external service or resource. They are used to allow pods within the cluster to access external services using a DNS name.
    
* **Headless Service:** Headless services are used when you want DNS records for individual pod IPs without load balancing. They are often associated with StatefulSets, where each pod has a unique identity.
    
* **Ingress:** Ingress is not a service type, but it's a resource used to manage external access to services based on HTTP routing rules. Ingress controllers handle the actual request routing and load balancing to services based on Ingress rules.
    

### 🔸 Can you explain the concept of self-healing in Kubernetes and give examples of how it works?

Self-healing in Kubernetes refers to the platform's ability to automatically detect and recover from failures or issues without human intervention. Here are some examples of how self-healing works:

* **Pod Restart:** If a pod becomes unhealthy due to application crashes or unresponsiveness, Kubernetes can automatically restart the pod to attempt recovery. You can specify health checks (readiness and liveness probes) in your pod configuration to define when a pod is considered healthy or not.
    
* **Node Replacement:** If a node in the cluster fails or becomes unresponsive, Kubernetes can automatically reschedule the pods that were running on that node to healthy nodes in the cluster. This ensures that the application remains available despite node failures.
    
* **Horizontal Pod Autoscaling (HPA):** HPA automatically adjusts the number of pod replicas based on resource utilization metrics (e.g., CPU or memory usage). When the load increases, HPA can add more replicas to handle the increased demand, and when the load decreases, it can scale down to save resources.
    
* **Rolling Updates:** When you perform updates to your application (e.g., deploying a new version of a container image), Kubernetes can perform rolling updates. It gradually replaces old pods with new ones, ensuring that the application remains available during the update process.
    

### 🔸 How does Kubernetes handle storage management for containers?

Kubernetes provides Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) to manage storage for containers:

* **Persistent Volumes (PVs):** PVs are physical storage resources provisioned by an administrator. They abstract the underlying storage infrastructure and can be NFS shares, cloud storage volumes, or other types of storage. PVs have a lifecycle independent of pods.
    
* **Persistent Volume Claims (PVCs):** PVCs are requests made by pods for storage resources. When a pod needs persistent storage, it creates a PVC specifying its requirements (e.g., size and access mode). Kubernetes binds PVCs to available PVs that match the requirements.
    
* **Storage Classes:** Storage classes define different classes of storage with various properties (e.g., performance levels). Users can request storage from a specific storage class in their PVC, and Kubernetes dynamically provisions the appropriate PV based on the storage class.
    
* **Volume Plugins:** Kubernetes supports various volume plugins that enable different types of storage backends, such as AWS EBS, Azure Disk, NFS, and more.
    

Using PVs and PVCs, Kubernetes allows containers to access and use persistent storage, ensuring data persistence even if pods are rescheduled to different nodes.

### 🔸 How does the NodePort service work?

The NodePort service type in Kubernetes exposes a service on a static port on each node's IP address. Here's how it works:

1. When you create a NodePort service, Kubernetes allocates a static port (in the range 30000-32767 by default) on each node in the cluster.
    
2. The service listens on this static port on each node.
    
3. When external traffic arrives at any node's IP address on the specified static port, that traffic is forwarded to one of the pods that the NodePort service is directing traffic to. The pod is chosen based on the defined service's selector.
    

NodePort services are often used when you need to expose a service to the external network, but it may not be suitable for production use without additional configuration, such as setting up an external load balancer in front of the nodes.

### 🔸 What is a multinode cluster and a single-node cluster in Kubernetes?

* **Multinode Cluster:** A multinode cluster in Kubernetes consists of multiple physical or virtual machines (nodes) that collectively form the Kubernetes cluster. Each node has its own resources (CPU, memory, storage) and runs Kubernetes components such as the kubelet, kube-proxy, and container runtime. Multinode clusters are typical in production environments and provide high availability, fault tolerance, and resource scalability.
    
* **Single-Node Cluster:** A single-node cluster is a Kubernetes cluster running on a single machine. It includes the same core components as a multinode cluster but lacks the redundancy and fault tolerance of a larger cluster. Single-node clusters are often used for development, testing, or learning purposes because they are simpler to set up but may not provide the same level of resilience as multinode clusters.
    

Single-node clusters are useful for local development and experimentation, but they do not offer the same production-level capabilities for high availability and scaling.

### 🔸 Difference between `create` and `apply` in Kubernetes?

In Kubernetes, both `kubectl create` and `kubectl apply` are commands used to create or update resources defined in YAML or JSON files. However, there are key differences between them:

* `kubectl create`**:**
    
    * Used for creating new resources.
        
    * If the resource already exists (based on the name specified in the YAML file), it will result in an error.
        
    * Typically used for creating resources that are meant to be created once and not updated.
        
* `kubectl apply`**:**
    
    * Used for creating and updating resources.
        
    * If the resource already exists, `kubectl apply` will update it based on the changes in the YAML file.
        
    * `kubectl apply` is commonly used for managing resources that may evolve or change over time, as it allows you to declaratively define the desired state of the resource.
        

The choice between `create` and `apply` depends on your use case. If you want to ensure that a resource is created but not modified once created, `kubectl create` is suitable. If you want to manage resources that may change or evolve, `kubectl apply` is the preferred choice, as it will update.

## 📍 Conclusion

I truly hope that this list of kubernetes interview questions has been incredibly helpful to you! 🎉🌟