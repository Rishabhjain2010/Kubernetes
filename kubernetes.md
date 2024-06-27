# **Documentation on Kubernetes (K8s)**

![Kubernetes](https://miro.medium.com/v2/resize:fit:1024/1*V8JWIC-tqYQkS1b1edsu3w.png)

## _Table of Contents_

1. [Introduction to Kubernetes](#introduction-to-kubernetes)
2. [Features of Kubernetes](#features-of-kubernetes)
3. [Kubernetes Components & Architecture](#kubernetes-components-and-architecture)
4. [Alternatives to Kubernetes](#alternatives-to-kubernetes)
5. [Installation & Setup](#installation--setup)
6. [Conclusion](#conclusion)

## **Introduction to Kubernetes**

- Kubernetes, also known as K8s, is an open-source container orchestration system for automating deployment, scaling, and management of containerized applications.
- It is a containerization, organization, and management tool.
- It is an open-source version of Borg by Google that was released in 2014.
- Kubernetes is also known as k8s, as k-ubernete-s, the "ubernete" is an 8-letter word, hence it is a shorter way of calling the long word.
- It is used to automate containerization scaling and management of containerized applications.

### What is containerization and why do we need it?

_A container is a virtual environment running on an OS, containing an application with other required resources and tools like its own file system, CPU, memory, process space, and more. A container is decoupled from the underlying infrastructure and hence it is portable across clouds and OS distributions._

In earlier times, when an application was hosted it was directly hosted to the server. When more than one application ran on the server, there arose a situation where all the resources available on the server might be utilized by a single application, leaving no resources for others to run. This was the situation in the traditional deployment era. To solve these problems, “Virtualization” was introduced. Virtualization allowed us to run multiple virtual machines (VMs) on a single physical server’s CPU. It allowed better resource management and isolation.

Since every individual application needed a separate version of the OS, the resources were being overutilized as well as wasted. Here comes the role of containerization and containers. Containers are similar to VMs, but they do not require individual OS and provide a relaxation on isolation introduced by VMs. Therefore, containers are considered lightweight and better to run on servers.

## **Features of Kubernetes**

- **Service Discovery and Load Balancing**: Kubernetes can expose containers using DNS names or their IP addresses. It can distribute network traffic evenly to ensure deployment stability, even under high traffic conditions.
- **Storage Orchestration**: Kubernetes allows automatic mounting of a storage system of your choice, such as local storage or public cloud providers.
- **Automated Rollouts and Rollbacks**: Kubernetes lets you define the desired state of your deployed containers and adjusts the actual state accordingly at a controlled pace. It can automatically create new containers, remove existing ones, and migrate resources to new containers as needed.
- **Automatic Bin Packing**: You provide Kubernetes with a cluster of nodes to run containerized tasks. By specifying the CPU and memory (RAM) requirements for each container, Kubernetes optimizes the placement of containers on your nodes to maximize resource utilization.
- **Self-Healing**: Kubernetes automatically restarts failed containers, replaces them, kills unresponsive containers, and ensures they are not advertised to clients until they are ready to serve.
- **Secret and Configuration Management**: Kubernetes enables secure storage and management of sensitive information like passwords, OAuth tokens, and SSH keys. It allows you to deploy and update secrets and application configurations without rebuilding container images or exposing secrets in stack configurations.
- **Batch Execution**: Kubernetes can manage batch and CI workloads, ensuring failed containers are replaced as needed.
- **Horizontal Scaling**: Easily scale your applications up or down via simple commands, a UI, or automatically based on CPU usage.
- **IPv4/IPv6 Dual-Stack**: Supports the allocation of both IPv4 and IPv6 addresses to Pods and Services.
- **Designed for Extensibility**: Kubernetes allows you to add new features to your cluster without altering the upstream source code.

## **Kubernetes Components & Architecture**

![Kubernetes Architecture](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg)

Kubernetes architecture consists of modular and highly scalable components like **Control Plane** and **Nodes**. Each part plays a crucial role in managing, scheduling, and running a containerized application.

### Control Plane Components

1. **API Server (kube-apiserver)**
   - The API server is the front-end for the Kubernetes control plane. It exposes the Kubernetes API, which is used by external and internal components to interact with the cluster. The API server handles REST operations and provides the interface for all the other components.

2. **etcd**
   - etcd is a consistent and highly-available key-value store used by Kubernetes for all cluster data storage. It stores configuration data, state data, and metadata. etcd serves as the source of truth for the cluster's state.

3. **Controller Manager (kube-controller-manager)**
   - The controller manager runs various controllers that regulate the state of the cluster. This includes the node controller (notices and responds when nodes go down), the replication controller (maintains the desired number of pods), and others.

4. **Scheduler (kube-scheduler)**
   - The scheduler assigns work to nodes by watching for newly created pods and selecting the best available node to run them. Decisions are based on resource requirements, policy constraints, and current workload.

### Worker Node Components


2. Worker Node Components:
Worker nodes are the machines (virtual or physical) where the containers are deployed and run. Each node has several components to manage containers and communicate with the control plane.

 - Kubelet:

   - An agent that runs on each worker node.
   - Ensures that containers are running in a Pod, interacts with the container runtime, and reports back to the control plane.

 - Kube-Proxy:

   - Maintains network rules on nodes, enabling network communication to and from Pods.
   - Implements service load balancing and network policies.

 - Container Runtime:

   - The software responsible for running containers (e.g., Docker, containerd, CRI-O).
   - Manages the container lifecycle and provides necessary resources.

3. Cluster-Level Components and Resources:

 - Pods:

   - The smallest and simplest Kubernetes objects.
   - A Pod represents a single instance of a running process and can contain one or more containers.

 - Services:

   - An abstraction that defines a logical set of Pods and a policy for accessing them.
   - Provides stable IP addresses and DNS names for Pods.

 - Volumes:

   - Directory accessible to containers in a Pod, used for persistent data storage.
   - Multiple types, including local storage, network storage, and cloud-based solutions.

 - Namespaces:

   - Provide a scope for names in the cluster, allowing for resource isolation and avoiding naming collisions.
   - Useful for dividing cluster resources among multiple users or teams.

 - ConfigMaps and Secrets:

   - ConfigMaps store non-confidential configuration data.
   - Secrets store sensitive information such as passwords, tokens, and SSH keys.
   - Both can be injected into Pods without rebuilding container images.

 - ReplicaSets:

   - Ensure a specified number of Pod replicas are running.
   - Provide resilience and scalability by maintaining the desired number of pods.

 - Deployments:

   - Manage ReplicaSets and facilitate declarative updates to applications.
   - Support rolling updates and rollbacks, making it easy to update applications without downtime.

4. Networking and Extensibility:

 - Networking:

   - Kubernetes manages networking through a flat network model, allowing all Pods to communicate with each other.
   - Network plugins (e.g., Calico, Flannel, Weave) implement networking policies and provide network isolation and security.

 - Ingress Controllers:
 
   - Manage external access to services, typically HTTP/HTTPS.
   - Provide features like load balancing, SSL termination, and name-based virtual hosting.

 - Custom Resource Definitions (CRDs):

   - Allow users to define custom resources to extend the Kubernetes API.
   - Enable the management of new types of resources specific to user needs without modifying the core Kubernetes code.

5. Cluster Workflow:
 
 - User Interaction:

   - Users interact with the Kubernetes API server using tools like kubectl to submit deployment configurations and manage resources.
 
 - Scheduling:

   - The scheduler monitors the state of the cluster and assigns Pods to nodes based on resource availability and requirements.

 - Pod Execution:

   - Kubelet on the worker nodes receives instructions to start Pods, interacting with the container runtime to launch containers.

 Networking and Services:

Kube-Proxy and network plugins manage networking rules, enabling communication between Pods and external clients.
Monitoring and Management:

Controller Manager and other control plane components continuously monitor the state of the cluster, ensuring the desired state is maintained, handling failures, and scaling resources as needed.
Kubernetes' architecture is designed for robustness, scalability, and extensibility, making it suitable for managing complex, containerized applications in dynamic environments.


## Alternative of Kubernetes


_**Kubernetes*-is a powerful and widely-used container orchestration platform, but there are several alternatives that offer different features and capabilities._

Here are some of the notable alternatives to Kubernetes

1. Docker Swarm:

 - Overview: Docker Swarm is a native clustering and scheduling tool for Docker containers. It turns a pool of Docker hosts into a single, virtual host.
 - Strengths: Simple to set up and use, tightly integrated with Docker, provides native clustering capabilities.
 - Use Cases: Smaller deployments, users already familiar with Docker, projects that require simplicity over extensive features.

2. Apache Mesos with Marathon:

 - Overview: Apache Mesos is a cluster manager that can manage large-scale clusters and run various distributed systems. Marathon is a container orchestration platform  that runs on Mesos.
 - Strengths: Highly scalable, supports multiple frameworks, strong in big data and analytics workloads.
 - Use Cases: Large-scale deployments, mixed workloads, environments requiring support for multiple container formats.

3. Nomad:

 - Overview: Nomad is a flexible, enterprise-grade cluster manager and scheduler from HashiCorp, designed to handle a variety of workloads.
 - Strengths: Simplicity, flexibility to run different types of workloads, integrates well with HashiCorp ecosystem (e.g., Consul, Vault).
 - Use Cases: Diverse workload environments, users looking for simplicity and flexibility, enterprises using other HashiCorp tools.

4. Rancher:

 - Overview: Rancher is a complete container management platform that simplifies Kubernetes deployment and management.
 - Strengths: User-friendly, multi-cluster management, extensive GUI, supports Kubernetes and other orchestration engines.
 - Use Cases: Enterprises seeking an easier Kubernetes management experience, multi-cluster environments.

5. OpenShift:

 - Overview: OpenShift is an enterprise Kubernetes platform by Red Hat that provides additional features and tools on top of Kubernetes.
 - Strengths: Enterprise-grade features, strong security and compliance, integrated CI/CD tools, developer-friendly.
 - Use Cases: Enterprises looking for comprehensive Kubernetes solutions with additional enterprise features and support.

6. Tanzu Kubernetes Grid (TKG):

 - Overview: Tanzu Kubernetes Grid is part of VMware’s Tanzu portfolio, offering Kubernetes clusters on VMware infrastructure and public clouds.
 - Strengths: Integration with VMware products, enterprise-grade support, hybrid and multi-cloud capabil ities.
 - Use Cases: VMware environments, enterprises needing robust Kubernetes management across hybrid clou ds .
 
7. ECS (Amazon Elastic Container Service): 

 - Overview: ECS is a fully managed container orchestration service by AWS that supports Docker containers.
 - Strengths: Deep integration with AWS services, easy to use with other AWS tools, no need to manage  c ontrol plane.
 - Use Cases: Workloads running in AWS, users wanting a fully managed service, AWS-centric environment s .

8. GKE (Google Kubernetes Engine):

 - Overview: GKE is a managed Kubernetes service by Google Cloud Platform (GCP).
 - Strengths: Fully managed, integrates well with GCP services, offers advanced features like auto-scaling, security, and logging.
 - Use Cases: Workloads running in GCP, users wanting a fully managed Kubernetes experience with advanced features.

9. AKS (Azure Kubernetes Service):

 - Overview: AKS is a managed Kubernetes service by Microsoft Azure.
 - Strengths: Fully managed, integrates well with Azure services, easy to use with other Azure tools.
 - Use Cases: Workloads running in Azure, users wanting a fully managed service, Azure-centric environments.

__**Each of these alternatives has its strengths and ideal use cases, so the best choice depends on the specific requirements of the project or organization, including scale, existing infrastructure, team expertise, and specific feature needs.**__


## Getting Started , Installation and Setup

### Prerequisites

1. Basic knowledge of Docker.
2. A system with a supported OS (Linux, macOS, or Windows).
3. Kubernetes command-line tool (kubectl) installed.

### Installation 

* _**Installing kubectl**_

    1. On macOS:

       ```s 
       brew install kubectl
       ```

    2. On Windows:
       ```s
       choco install kubernetes-cli
       ```

    3. On Linux:
       ```s
       snap install kubectl --classic
       ```
* _**Setting Up a Kubernetes Cluster**_

 - Using Minikube (for local development):
    
    Minikube is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your local machine for users looking to try out Kubernetes or develop with it day-to-day.
    
    1. Install Minikube:

        ◦ On macOS:
          ```s
          brew install minikube
          ```
        ◦ On Windows:
          ```s
          choco install minikube
          ```
        ◦ On Linux:
          ```s
          sudo apt install curl
          curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
          sudo install minikube-linux-amd64 /usr/local/bin/minikube
          
          ```

    2. Start Minikube:
       ```s
        minikube start
       ```

    3. Verify the Cluster:
       ```s
       kubectl get nodes
       ```

### Deploying Applications

* _**Create a Deployment**_

  ```s
  kubectl create deployment nginx --image=nginx
  #This command creates a Deployment named nginx that uses the nginx Docker image.
  ```

* _**Expose the Deployment**_
  ```s
  kubectl expose deployment nginx --port=80 --type=NodePort
  #This command creates a Service to expose the nginx Deployment on port 80.
  ```

* _**Get the Service URL**_

  ```s
  minikube service nginx --url
  #This command returns the URL to access the nginx service.
  ```

### Managing the Cluster

* _**Scaling Applications**_

_Scaling adjusts the number of replicas in your Deployment. For example:_

* _**Scale Up/Down a Deployment**_
       
  ```s
  kubectl scale deployment nginx --replicas=4
  #This command scales the nginx Deployment to 4 replicas.
  ```

* _**Check the Status**_
       
  ```s
  kubectl get deployments
  #This command displays the current state of Deployments, including the number of desired and available replicas.
  ```

### Updating Applications

* _**Update the Image of a Deployment**_
       
 ```s
 kubectl set image deployment/nginx nginx=nginx:1.16
 #This command updates the nginx Deployment to use the nginx:1.16 image.
 ```

* _**Check the Rollout Status**_
       
 ```s
 kubectl rollout status deployment/nginx
 #This command checks the status of the update.
 ```

* _**Rollback in Case of Issues**_

 ```s
 kubectl rollout undo deployment/nginx
 #This command rolls back the nginx Deployment to the previous version.
 ```

### Useful Commands

  *  _**View Cluster Info**_
     
      ```s
      kubectl cluster-info
      #This command displays cluster information.
      ```

  * _**View Nodes**_
     
      ```s
      kubectl get nodes
      #This command lists all nodes in the cluster.
      ```

  *  _**View Pods**_
    
      ```s
      kubectl get pods
      #This command lists all Pods in the cluster.
      ```

  * _**Describe a Pod**_

      ```s    
      kubectl describe pod <pod-name>
      #This command provides detailed information about a specific Pod.
      ```

  *  _**Delete a Deployment**_

      ```s
      kubectl delete deployment nginx
      #This command deletes the nginx Deployment.
      ```


## Getting Started

### Starting  Kubernetes Locallay

Let’s test our local Kubernetes installation.

    kubectl cluster-info

### Running Kubectl


#### Current context

Get the current context:

    kubectl config current-context

#### List all contexts

List all the contexts:

    kubectl config get-contexts

#### Change context

Use a context:

    kubectl config use-context [contextName]

#### Using kubectx

What's great about Kubernetes is the incredible amount of tools created by the community and available for free.  Kubectx is a simple tool that provides an easy way to list and change context.

You can install it on:

Windows (if you have Chocolatey installed):

    choco install kubectx-ps

macOS (if you have Brew installed):

    brew install kubectx

Ubuntu:

    sudo apt install kubectx

To list the contexts, simply type:

    kubectx

To change context:

    kubectx <contextName>

#### Rename context

Rename context:

    kubectl config rename-context [old-name] [new-name]

#### Delete context

Delete context:

    kubectl config delete-context [contextName]

### Cointainer Deployement

_In K8s container can be deployed using two methods:_
1. _Imperative_
2. _Declarative_

Let's deploy an Nginx container using both methods.

#### Imperative

    kubectl create deployment nginx1 --image=nginx

#### Declarative

    kubectl create -f deploy-example.yaml
    

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
      env: prod
  template:
    metadata:
      labels:
        app: nginx
        env: prod
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi        
        ports:
        - containerPort: 80
```

#### Cleanup

    kubectl delete deployment nginx1
    kubectl delete deploy nginx2

### Namespaces

#### Get namespaces

Open a terminal and get the currently configured namespaces.

    kubectl get namespaces
    kubectl get ns

#### Get the pods list

Get a list of all the installed pods.

    kubectl get pods

You get the pods from the default namespace.  Try getting the pods from the docker namespace.  You will get a different list.

    kubectl get pods --namespace=kube-system
    kubectl get pods -n kube-system

#### Change namespace

Change the namespace to the docker one and get the pods list.

    kubectl config set-context --current --namespace=kube-system

#### Get the pods

    kubectl get pods

#### Now change back to the default namespace

    kubectl config set-context --current --namespace=default
    kubectl get pods

#### Create and delete a namespace

    kubectl create ns [name]
    kubectl get ns
    kubectl delete ns [name]

### Nodes

#### Getting Nodes Information

Get a list of all the installed nodes. Using Docker Desktop, there should be only one.

    kubectl get nodes

Get some info about the node.

    kubectl describe node

### Pods

Let’s first create a node running Nginx by using the imperative way.

#### Create the pod

    kubectl run mynginx --image=nginx

#### Get a list of running pods

    kubectl get pods

#### Get more info

    kubectl get pods -o wide
    kubectl describe pod mynginx

#### Delete the pod

    kubectl delete pod mynginx

#### Create a pod running BusyBox

Let’s now create a node running BusyBox, this time attaching bash to our terminal.

    kubectl run mybox --image=busybox -it -- /bin/sh

#### List the folders and use command

    ls
    echo -n 'A Secret' | base64
    exit

#### Cleanup

    kubectl delete pod mybox

#### Create a pod using the declarative way

Let’s now create a node using a YAML file.

    kubectl create -f myapp.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
  - name: nginx-container
    image: nginx
    resources:
      requests:
        cpu: 100m
        memory: 128Mi
      limits:
        cpu: 250m
        memory: 256Mi    
    ports:
    - containerPort: 80
      name: http
      protocol: TCP
    env:
    - name: DBCON
      value: myconnectionstring
```

#### Get some info

    kubectl get pods -o wide
    kubectl describe pod myapp-pod

#### Attach our terminal

    kubectl exec -it myapp-pod -- bash

Print the DBCON environment variable that was set in the YAML file.

    echo $DBCON

#### Detach from the instance

    exit

#### Cleanup

    kubectl delete -f myapp.yaml


## Conclusion

_**Kubernetes is a powerful system for managing containerized applications in a clustered environment. This guide covers the basics of setting up and managing a Kubernetes cluster, deploying and managing applications, and scaling and updating them. To explore more advanced features, consider reading the official Kubernetes documentation.**_
































