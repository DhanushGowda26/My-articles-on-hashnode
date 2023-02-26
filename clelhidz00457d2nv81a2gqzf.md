# Introduction to Kubernetes

### Overview of Kubernetes

Kubernetes (K8s) is an open-source container orchestration system that was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). K8s is designed to automate the deployment, scaling, and management of containerized applications, and it has become the de facto standard for managing containers in production environments.

K8s was developed in response to the challenges of managing large-scale containerized systems. As the use of containers became more widespread, it became increasingly difficult to manage them manually. Each container has its own set of dependencies and requirements, and as the number of containers in a system grows, it becomes harder to manage them and ensure they are running smoothly.

K8s addresses this challenge by providing a platform for managing containerized applications at scale. It automates many of the tasks associated with managing containers, such as load balancing, service discovery, and networking. K8s also provides built-in features for fault tolerance and self-healing, which means that the system can automatically recover from failures without human intervention.

K8s started as an internal Google project called Borg, which was used to manage Google's vast network of services and applications. Borg was highly successful, but it was not designed to be used outside of Google. In 2014, Google released K8s as an open-source project, based on the lessons learned from Borg.

Since then, K8s has become the most popular container orchestration system, with widespread adoption across a variety of industries and use cases. K8s has become an essential tool for managing containerized applications in production environments, as it provides a platform for automating many of the tasks associated with managing containers, and it helps to reduce complexity and increase the reliability of applications.

### Cluster

A cluster in Kubernetes, a cluster is a set of physical or virtual machines, also known as nodes, that are connected together and run containerized applications. It consists of a control plane and worker nodes. The control plane is responsible for managing and coordinating the worker nodes, which are responsible for running the actual workloads.

### Cluster Components

Control plane: The control plane is responsible for managing the overall state of the cluster, including scheduling workloads, scaling applications, and monitoring the health of nodes and services. It includes several different components, including the API server, etcd, scheduler, and controller manager.

Nodes: Nodes are the individual machines that make up the cluster. They run the workloads and services that are deployed to the cluster and communicate with the control plane to receive instructions and updates.

Container runtime: Container runtime is a software component responsible for running containers on a system. It is an implementation of the container specification, which defines the interface between the container and the host operating system. The container runtime is responsible for managing the lifecycle of containers, including starting and stopping them, managing their resource usage, and providing access to the container's filesystem

Control manager: The control manager in Kubernetes is responsible for maintaining the desired state of the cluster. It is comprised of several components that are responsible for different aspects of the cluster:

1. Node Controller: Monitors the state of each node in the cluster and takes action if a node goes down or becomes unreachable.
    
2. Replication Controller: Ensures that the desired number of replicas of a pod are running in the cluster.
    
3. Endpoints Controller: Populates the endpoints object (which contains information about the IP addresses and ports of the pods that a service is targeting) based on the current state of the cluster.
    
4. Service Account & Token Controllers: Manage the creation and deletion of service accounts and their associated tokens.
    
5. Namespace Controller: Ensures that namespaces are created and deleted as necessary.
    
6. Resource Quota Controller: Enforces resource quotas (such as CPU and memory limits) for namespaces and individual pods.
    

The control manager continuously monitors the state of the cluster and takes action to ensure that the current state matches the desired state specified in the Kubernetes API. It interacts with the API server to create, update, and delete resources as necessary.

For example, if a pod crashes or becomes unresponsive, the Replication Controller will detect this and automatically create a new pod to replace it. Similarly, if a node becomes unreachable, the Node Controller will mark the node as unavailable and reschedule any pods running on that node to other available nodes in the cluster.

In short, the control manager is responsible for maintaining the overall health and functionality of the Kubernetes cluster by monitoring the state of the cluster and taking corrective action as necessary.

Kubelet: Kublet is an agent that runs on each node in a Kubernetes cluster. Its primary responsibility is to ensure that the containers running on its node are healthy and running as expected. It communicates with the Kubernetes control plane to receive instructions on which pods should be running on the node, and then starts, stops, or restarts the necessary containers to maintain the desired state.

Kubelet also performs other tasks, such as monitoring the health of the node and reporting back to the control plane, pulling container images from a registry, and managing the storage volumes used by containers. Essentially, Kubelet is the node-level supervisor for Kubernetes.

Kube-Proxy: Kube-Proxy is a component of Kubernetes that runs on each worker node and is responsible for managing network communications between the services and the pods running on that node. It acts as a network proxy and load balancer for the services running in the Kubernetes cluster.

Kube-proxy ensures that each pod can communicate with other pods in the same service, as well as other services in the cluster. It also handles load balancing of traffic to the pods in the service, distributing requests evenly among them.

Kube-proxy uses various networking modes like User-Space, IPTables, and IPVS to provide these functionalities. It monitors the Kubernetes API server for changes to services and endpoints and updates its routing tables accordingly.

Example: Let's say you have a Kubernetes Service called "my-service" that exposes a set of pods that are running a web application. When a client makes a request to "my-service", kube-proxy is responsible for routing that request to one of the pods that is running the web application.

To do this, kube-proxy uses a few different mechanisms. One way is by creating iptables rules that map the Service's IP address and port to the IP addresses and ports of the pods that are running the web application. This allows incoming traffic to be load balanced across multiple pods, providing high availability and scalability for your application.

Another way kube-proxy works is by using the "userspace" proxy mode. In this mode, kube-proxy listens on the Service's IP address and port, and when it receives a request, it opens a connection to one of the pods that is running the web application and forward the request over that connection. This mode can be slower and less efficient than the iptables mode, but it can be useful in some situations where iptables are not available.

Overall, kube-proxy plays an important role in making Kubernetes Services work correctly and efficiently, by routing incoming traffic to the appropriate pods and providing load balancing and high availability for your application.

Ingress: Kubernetes Ingress is a way to expose HTTP and HTTPS routes from outside the cluster to services within the cluster. It provides load balancing, SSL termination, and path-based routing for incoming traffic.

Networking: Networking is a critical component of any cluster, as it enables the communication between nodes and services. Kubernetes uses a software-defined networking (SDN) approach, which means that the network is implemented entirely in software and can be dynamically configured and managed.

Storage: Storage is also an important component of a Kubernetes cluster, as it allows data to be persisted and accessed by applications and services. Kubernetes supports several different types of storage, including local storage, network-attached storage (NAS), and storage area networks (SANs).

Each of these components has its own roles and responsibilities and works together to provide a highly available and scalable platform for running containerized workloads. The control plane is responsible for managing the overall state of the cluster, while nodes are responsible for running workloads and services. Networking provides the communication fabric between nodes and services, while storage allows data to be persisted and accessed.

Overall, a Kubernetes cluster is designed to be highly modular and flexible, so that it can be tailored to meet the needs of a wide range of different applications and workloads

Each of these components has its own roles and responsibilities and works together to provide a highly available and scalable platform for running containerized workloads. The control plane is responsible for managing the overall state of the cluster, while nodes are responsible for running workloads and services. Networking provides the communication fabric between nodes and services, while storage allows data to be persisted and accessed.

Overall, a Kubernetes cluster is designed to be highly modular and flexible, so that it can be tailored to meet the needs of a wide range of different applications and workloads

### Controle Plane Articheture

API server: The API server is the main management point for the cluster. It exposes a REST API that can be used to interact with the cluster and is responsible for validating and processing requests. Whenever an administrator, developer or user wants to interact with the cluster, they send a request to the API server. The API server then takes that request and either validate it or rejects it based on the cluster's configuration.

etcd: etcd is a distributed key-value store that is used to store the state of the cluster. It is highly available and fault-tolerant, and provides a consistent view of the cluster's state across all nodes. Whenever a component in the control plane or a worker node makes a change to the cluster's state, that change is recorded in etcd. Other components can then read that information from etcd, ensuring that all components have a consistent view of the cluster's state.

Controller manager: The controller manager is responsible for ensuring that the desired state of the cluster is maintained. It includes several different controllers, such as the replication controller and the node controller, that monitor the state of the cluster and take action if necessary. For example, if a worker node fails, the node controller will take action to reschedule the pods running on that node onto other nodes in the cluster. The controller manager continually monitors the state of the cluster and takes action as needed to ensure that the desired state is maintained.

Scheduler: The scheduler is responsible for assigning workloads to nodes in the cluster. It takes into account factors such as resource availability and workload constraints to ensure that workloads are scheduled in the most efficient way possible. For example, if a pod requires a certain amount of memory or CPU, the scheduler will ensure that it is only scheduled onto nodes that have enough resources available. The scheduler constantly monitors the state of the cluster and assigns workloads to nodes as resources become available.

All of these components work together to manage the state of the Kubernetes objects, like pods, services, and deployments. The API server is the main interface for interacting with the cluster, while etcd provides a consistent view of the cluster's state. The controller manager and scheduler ensure that workloads are running correctly and efficiently. By working together, these components ensure that the cluster is always running in the desired state, and that applications and services are available to users at all times.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677419983663/cf2ff1cf-c51a-4189-98b0-110f4f89a457.png align="center")

### Kubernetes Objects

In Kubernetes, an object is a persistent entity that represents the state of the cluster. Every object in Kubernetes has a set of properties, such as a name, labels, and annotations, which are used to uniquely identify and manage the object.

Each object in Kubernetes is defined using a YAML or JSON configuration file, which specifies the object's properties and behaviour. These configuration files can be used to create, update, or delete objects in the cluster using the kubectl command-line tool or other Kubernetes APIs.

There are many different types of objects in Kubernetes, each with its own set of properties and behaviours. Here are a few examples:

Pod: A Pod is the smallest deployable unit in Kubernetes. It is a logical host for one or more containers. All containers in a Pod share the same network namespace, IP address, and port space, and can communicate with each other using localhost.

Here's an example YAML file for creating a Pod in Kubernetes:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

This YAML file creates a Pod named my-pod that runs a single container named nginx-container, which uses the latest version of the nginx image. The container listens on port 80.

Service: A service is an abstraction that represents a set of pods that perform the same function. Services provide a stable IP address and DNS name for a set of pods and allow other parts of your application to communicate with the pods.

Here's an example YAML file for creating a Service in Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - name: http
    port: 80
    targetPort: 80
  type: ClusterIP
```

This YAML file creates a Service named nginx-service that selects Pods with the label app=nginx. The Service listens on port 80 and forwards traffic to the same port on the Pods. The type of Service is ClusterIP, which means it provides a stable IP address for the set of Pods within the cluster.

Deployment: A deployment is a higher-level object that manages the lifecycle of a set of pods. Deployments allow you to update your application without downtime, by gradually replacing old pods with new ones. It provides declarative updates for Pods and ReplicaSets. A ReplicaSet is a group of identical Pods that are created and managed by a Deployment.

Here's an example YAML file for creating a Deployment in Kubernetes:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

This YAML file creates a Deployment named nginx-deployment that manages a set of 3 replicas of the nginx Pod. The selector specifies that the Deployment manages Pods with the label app=nginx. The template specifies the configuration for the Pods managed by the Deployment, which is the same as the configuration for the Pod we created earlier.

Namespace: A namespace is a way to divide a Kubernetes cluster into multiple virtual clusters. Namespaces allow different teams or projects to use the same cluster, without interfering with each other.

Here's an example YAML file that sets up two namespaces, `project-a` and `project-b`, with corresponding labels:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: project-a
  labels:
    project: project-a
---
apiVersion: v1
kind: Namespace
metadata:
  name: project-b
  labels:
    project: project-b
```

ConfigMap: A ConfigMap is an object in Kubernetes that allows you to store configuration data separately from your code. This makes it easy to manage configuration data across different environments or to update configuration data without having to rebuild your application. ConfigMaps can be used to store data like environment variables, command-line arguments, or configuration files.

In our example, let's say we want to store the URL of the database server in a ConfigMap. We can create a ConfigMap with the following YAML file:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: example-config
data:
  DB_URL: "db.example.com"
```

We can then reference the value of the `DB_URL` key in our application code or in other Kubernetes objects by using the ConfigMap. For example, if we have a Deployment that uses this ConfigMap, we can set the `DB_URL` environment variable like this:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
      - name: example-container
        image: example-image
        env:
        - name: DB_URL
          valueFrom:
            configMapKeyRef:
              name: example-config
              key: DB_URL
```

Here, we're using the `valueFrom` field to get the value of `DB_URL` from the ConfigMap.

Secret: A Secret is similar to a ConfigMap in that it allows you to store sensitive data like passwords, API keys, or TLS certificates. However, Secrets are encrypted at rest and in transit, so they provide an extra layer of security for sensitive data.

In our example, let's say we want to store the password for the database server in Secret. We can create a Secret with the following YAML file:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: example-secret
type: Opaque
data:
  password: <base64-encoded-password>
```

Note that the password is base64-encoded for security. We can then reference the value of the `password` key in our application code or in other Kubernetes objects by using the Secret. For example, if we have a Deployment that uses this Secret, we can set the `DB_PASSWORD` environment variable like this:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: example
    spec:
      containers:
      - name: example-container
        image: example-image
        env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: example-secret
              key: password
```

Here, we're using the `valueFrom` field to get the value of `password` from the Secret.

### Kubectl:

kubectl is a command-line interface tool for Kubernetes that allows you to interact with a Kubernetes cluster. It is not a terminal itself, but rather a program that you can run in a terminal window to execute commands against a Kubernetes cluster.

kubectl provides a way to create, modify, and manage Kubernetes objects such as pods, services, and deployments. With kubectl, you can inspect the state of the cluster, deploy new applications, update existing applications, and scale resources up or down as needed.

To use kubectl, you need to have access to a Kubernetes cluster and have kubectl installed on your local machine. Once you have these requirements met, you can use the kubectl command to connect to the cluster and run commands against it.

Overall, kubectl is a powerful tool for managing and interacting with Kubernetes clusters, and it is commonly used by developers, system administrators, and other IT professionals who work with Kubernetes.

Here are a few examples of how you can use kubectl:

1. To get the list of all pods in the cluster, you can use the following command:
    
    ```bash
    kubectl get pods
    ```
    
2. To create a deployment from a YAML file, you can use the following command
    
    ```bash
    kubectl create -f deployment.yaml
    ```
    
3. To scale up the number of replicas in a deployment, you can use the following command:
    
    ```bash
    kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>
    ```
    
4. To view the logs of a pod, you can use the following command:
    
    ```bash
    kubectl logs <pod-name>
    ```
    
5. To create a new service, you can use the following command:
    
    ```bash
    kubectl create service <service-type> <service-name> --tcp=<port>:<target-port>
    ```
    

[Install Kubectl](https://kubernetes.io/docs/tasks/tools/)

### Minikube:

Minikube is a tool that enables you to run a single-node Kubernetes cluster on your local machine. It creates a virtual machine that runs a lightweight version of the Kubernetes control plane and allows you to deploy and test Kubernetes applications without needing access to a full-blown production Kubernetes cluster.

Minikube provides an easy way for developers to experiment with Kubernetes and test their applications in a local environment before deploying them to a production cluster. It can also be used to learn Kubernetes concepts and features and to develop and debug Kubernetes-related code.

With Minikube, you can easily spin up a local Kubernetes cluster with just a few commands, and then use kubectl to deploy and manage your applications on the cluster. Since it runs locally on your machine, you don't need an internet connection or any special hardware to use Minikube.

Overall, Minikube is a useful tool for developers and anyone who wants to learn or experiment with Kubernetes, as it provides a simple and convenient way to run and test Kubernetes applications on a local machine.

[Install minikube](https://minikube.sigs.k8s.io/docs/start/)

Thanks for spending time in learning.