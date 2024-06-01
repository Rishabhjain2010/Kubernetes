#**Documentation on Kubernetes (K8)**
=


## _Table of Contents_



1. Introduction to Kubernetes
2. Features of Kubernetes 
3. Kubernetes Components
4. Alternative of Kubernetes
5. Instalation & Setup
6. 


## **Introduction to Kubernetes**
=

-Kubernetes also knows as K8s, K8s, is an open source system for automating deployement , scaling and management of containerized applications. 

-It is a containerization , organization and management tool. 
 
-It is a open source version of Borg by google that was relaeased in 2014.

-Kubernetes is also known as k8s, as k - ubernate - s , the ubernete is a 8 letter long word hence it is a shorter way of calling long word.

-It is used to automate containerization scalling and management of containerez applications. \


### What is containerization and why do we need it?

_A Container is as virtaul enviorment running on a OS, containing an application with other required resources and tools like its own file system , CPU , memory , process space and more. A container is decoupled from underlying infrastructer and hence it is portable across clounds and OS Distribution._


In early time, when a application was hosted it was directly hosted to the server and in a situation when more then one application runs on server, there arrives a situaton where all the resources avaialable on server may be utilised by a single application itself leaving no resoruces for other to run. This was the situation in tradidtional deployment era. To solve the underlying problems “Virtualization” was introduced. Virtualization allowed us to run multiple Virtual Machines on a single physical server’s CPU. It allowed better resource management and isolation.
Since, every individual application needed a seprate version of OS the resoruces were being over utilized as well as wasted. Here comes in olay the containerization and containers. Containers are simillar to VMs , but they do not require indiviual OS and provide a relaxation on isolation theat were introduced by VMs,  therefore containers are considered lightweight and better to run on servers. 

## **Features of Kubernetes**


* *Service Discovery and Load Balancing*: Kubernetes can expose containers using DNS names or their IP addresses. It can distribute network traffic evenly to ensure deployment stability, even under high traffic conditions.

* *Storage Orchestration*: Kubernetes allows automatic mounting of a storage system of your choice, such as local storage or public cloud providers.

* *Automated Rollouts and Rollbacks*: Kubernetes lets you define the desired state of your deployed containers and adjusts the actual state accordingly at a controlled pace. It can automatically create new containers, remove existing ones, and migrate resources to new containers as needed.

* *Automatic Bin Packing*: You provide Kubernetes with a cluster of nodes to run containerized tasks. By specifying the CPU and memory (RAM) requirements for each container, Kubernetes optimizes the placement of containers on your nodes to maximize resource utilization.

* *Self-Healing*: Kubernetes automatically restarts failed containers, replaces them, kills unresponsive containers, and ensures they are not advertised to clients until they are ready to serve.

* *Secret and Configuration Management*: Kubernetes enables secure storage and management of sensitive information like passwords, OAuth tokens, and SSH keys. It allows you to deploy and update secrets and application configurations without rebuilding container images or exposing secrets in stack configurations.

* *Batch Execution*: Kubernetes can manage batch and CI workloads, ensuring failed containers are replaced as needed.

* *Horizontal Scaling*: Easily scale your applications up or down via simple commands, a UI, or automatically based on CPU usage.

* *IPv4/IPv6 Dual-Stack*: Supports the allocation of both IPv4 and IPv6 addresses to Pods and Services.

* *Designed for Extensibility*: Kubernetes allows you to add new features to your cluster without altering the upstream source code.


## **Kubernetes Components and Architecture**



<img src="https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg">


_Kubernetes Architecture consists of many modular and highly scaleable components like **Control Plane** and **Nodes**. Every part playing a very crucial role in managing , scheduling , running a containerized application._


1. Control Plane Components:

  The control plane is responsible for managing the overall state of the cluster, maintaining the desired state of applications, and orchestrating tasks.

   * API Server (kube-apiserver):

    * The front-end of the Kubernetes control plane.
    * Exposes the Kubernetes API, handling REST operations, and acting as the primary interface for users and cluster components.

   * etcd:

    * A distributed, consistent key-value store.
    * Stores all cluster data, including configuration data, state information, and metadata.
    
   * Controller Manager (kube-controller-manager):

    *  Runs various controllers that regulate the state of the cluster.
    * Includes node controller (notices and responds when nodes go down), replication controller (maintains the desired number of pods), and others.

   * Scheduler (kube-scheduler):

    * Assigns work to nodes by watching for newly created pods and selecting the best available node to run them.
    * Decisions are based on resource requirements, policy constraints, and current workload.


2. Worker Node Components:
Worker nodes are the machines (virtual or physical) where the containers are deployed and run. Each node has several components to manage containers and communicate with the control plane.

Kubelet:

An agent that runs on each worker node.
Ensures that containers are running in a Pod, interacts with the container runtime, and reports back to the control plane.
Kube-Proxy:

Maintains network rules on nodes, enabling network communication to and from Pods.
Implements service load balancing and network policies.
Container Runtime:

The software responsible for running containers (e.g., Docker, containerd, CRI-O).
Manages the container lifecycle and provides necessary resources.

3. Cluster-Level Components and Resources:
Pods:

The smallest and simplest Kubernetes objects.
A Pod represents a single instance of a running process and can contain one or more containers.
Services:

An abstraction that defines a logical set of Pods and a policy for accessing them.
Provides stable IP addresses and DNS names for Pods.
Volumes:

Directory accessible to containers in a Pod, used for persistent data storage.
Multiple types, including local storage, network storage, and cloud-based solutions.
Namespaces:

Provide a scope for names in the cluster, allowing for resource isolation and avoiding naming collisions.
Useful for dividing cluster resources among multiple users or teams.
ConfigMaps and Secrets:

ConfigMaps store non-confidential configuration data.
Secrets store sensitive information such as passwords, tokens, and SSH keys.
Both can be injected into Pods without rebuilding container images.
ReplicaSets:

Ensure a specified number of Pod replicas are running.
Provide resilience and scalability by maintaining the desired number of pods.
Deployments:

Manage ReplicaSets and facilitate declarative updates to applications.
Support rolling updates and rollbacks, making it easy to update applications without downtime.

4. Networking and Extensibility:
Networking:

Kubernetes manages networking through a flat network model, allowing all Pods to communicate with each other.
Network plugins (e.g., Calico, Flannel, Weave) implement networking policies and provide network isolation and security.
Ingress Controllers:

Manage external access to services, typically HTTP/HTTPS.
Provide features like load balancing, SSL termination, and name-based virtual hosting.
Custom Resource Definitions (CRDs):

Allow users to define custom resources to extend the Kubernetes API.
Enable the management of new types of resources specific to user needs without modifying the core Kubernetes code.
Cluster Workflow:
User Interaction:

Users interact with the Kubernetes API server using tools like kubectl to submit deployment configurations and manage resources.
Scheduling:

The scheduler monitors the state of the cluster and assigns Pods to nodes based on resource availability and requirements.
Pod Execution:

Kubelet on the worker nodes receives instructions to start Pods, interacting with the container runtime to launch containers.
Networking and Services:

Kube-Proxy and network plugins manage networking rules, enabling communication between Pods and external clients.
Monitoring and Management:

Controller Manager and other control plane components continuously monitor the state of the cluster, ensuring the desired state is maintained, handling failures, and scaling resources as needed.
Kubernetes' architecture is designed for robustness, scalability, and extensibility, making it suitable for managing complex, containerized applications in dynamic environments.


## Alternative of Kubernetes


_**Kubernetes** is a powerful and widely-used container orchestration platform, but there are several alternatives that offer different features and capabilities._

Here are some of the notable alternatives to Kubernetes

1. Docker Swarm:

* Overview: Docker Swarm is a native clustering and scheduling tool for Docker containers. It turns a pool of Docker hosts into a single, virtual host.
* Strengths: Simple to set up and use, tightly integrated with Docker, provides native clustering capabilities.
* Use Cases: Smaller deployments, users already familiar with Docker, projects that require simplicity over extensive features.

2. Apache Mesos with Marathon:

* Overview: Apache Mesos is a cluster manager that can manage large-scale clusters and run various distributed systems. Marathon is a container orchestration platform that runs on Mesos.
* Strengths: Highly scalable, supports multiple frameworks, strong in big data and analytics workloads.
* Use Cases: Large-scale deployments, mixed workloads, environments requiring support for multiple container formats.

3. Nomad:

* Overview: Nomad is a flexible, enterprise-grade cluster manager and scheduler from HashiCorp, designed to handle a variety of workloads.

* Strengths: Simplicity, flexibility to run different types of workloads, integrates well with HashiCorp ecosystem (e.g., Consul, Vault).
* Use Cases: Diverse workload environments, users looking for simplicity and flexibility, enterprises using other HashiCorp tools.

4. Rancher:

* Overview: Rancher is a complete container management platform that simplifies Kubernetes deployment and management.
* Strengths: User-friendly, multi-cluster management, extensive GUI, supports Kubernetes and other orchestration engines.
* Use Cases: Enterprises seeking an easier Kubernetes management experience, multi-cluster environments.

5. OpenShift:

* Overview: OpenShift is an enterprise Kubernetes platform by Red Hat that provides additional features and tools on top of Kubernetes.
* Strengths: Enterprise-grade features, strong security and compliance, integrated CI/CD tools, developer-friendly.
* Use Cases: Enterprises looking for comprehensive Kubernetes solutions with additional enterprise features and support.

6. Tanzu Kubernetes Grid (TKG):

* Overview: Tanzu Kubernetes Grid is part of VMware’s Tanzu portfolio, offering Kubernetes clusters on VMware infrastructure and public clouds.
* Strengths: Integration with VMware products, enterprise-grade support, hybrid and multi-cloud capabilities.
* Use Cases: VMware environments, enterprises needing robust Kubernetes management across hybrid clouds.

7. ECS (Amazon Elastic Container Service):

* Overview: ECS is a fully managed container orchestration service by AWS that supports Docker containers.
* Strengths: Deep integration with AWS services, easy to use with other AWS tools, no need to manage control plane.
* Use Cases: Workloads running in AWS, users wanting a fully managed service, AWS-centric environments.

8. GKE (Google Kubernetes Engine):

* Overview: GKE is a managed Kubernetes service by Google Cloud Platform (GCP).
* Strengths: Fully managed, integrates well with GCP services, offers advanced features like auto-scaling, security, and logging.
* Use Cases: Workloads running in GCP, users wanting a fully managed Kubernetes experience with advanced features.

9. AKS (Azure Kubernetes Service):

* Overview: AKS is a managed Kubernetes service by Microsoft Azure.
* Strengths: Fully managed, integrates well with Azure services, easy to use with other Azure tools.
* Use Cases: Workloads running in Azure, users wanting a fully managed service, Azure-centric environments.

__**Each of these alternatives has its strengths and ideal use cases, so the best choice depends on the specific requirements of the project or organization, including scale, existing infrastructure, team expertise, and specific feature needs.**__


## Getting Started , Installation and Setup























