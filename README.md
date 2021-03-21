###### Kubernetes 

<img src="images/Kubernetes Architecture.png" width="500" height="300" />


## What is a Kubernetes cluster?

A Kubernetes cluster is a set of nodes that run containerized applications. Containerizing applications packages an app with its dependences and some necessary services. They are more lightweight and flexible than virtual machines. In this way, Kubernetes clusters allow for applications to be more easily developed, moved and managed. 

Kubernetes clusters allow containers to run across multiple machines and environments: virtual, physical, cloud-based, and on-premises. Kubernetes containers are not restricted to a specific operating system, unlike virtual machines. Instead, they are able to share operating systems and run anywhere.

Kubernetes clusters are comprised of one master node and a number of worker nodes. These nodes can either be physical computers or virtual machines, depending on the cluster.

The master node controls the state of the cluster; for example, which applications are running and their corresponding container images. The master node is the origin for all task assignments. It coordinates processes such as:

                * Scheduling and scaling applications
                * Maintaining a cluster’s state
                * Implementing update


## What makes up a Kubernetes cluster?

A Kubernetes cluster contains six main components:

# API Server:
* API server: In Kubernetes, everything is an API call served by the Kubernetes API server (kube-apiserver). The API server is a gateway to an etcd datastore that maintains the desired state of your application cluster. To update the state of a Kubernetes cluster, you make API calls to the API server describing your desired state.

# Scheduler:
* Scheduler: Places containers according to resource requirements and metrics. Makes note of Pods with no assigned node, and selects nodes for them to run on.

# Controller manager
* Controller manager: Runs controller processes and reconciles the cluster’s actual state with its desired specifications. Manages controllers such as node     controllers,  endpoints controllers and replication controllers.

# Kubelet:
* Kubelet: Ensures that containers are running in a Pod by interacting with the Docker engine , the default program for creating and managing containers. Takes a set of provided PodSpecs and ensures that their corresponding containers are fully operational.

# Pods:
* Pods : A Pod is the atom of Kubernetes — the smallest deployable object for building applications. A single Pod represents a running workload in your cluster and encapsulates one or more Docker containers, any required storage, and a unique IP address. Containers that make up a pod are designed to be co-located and scheduled on the same machine.

# Nodes:
* Nodes : Nodes are the machines running the Kubernetes cluster. These can be bare metal, virtual machines, or anything else. The word hosts is often used interchangeably with Nodes. I will try and use the term Nodes with consistency but will sometimes use the word Virtual Machine to refer to Nodes depending on context.

# Kube-Proxy:
* Kube-proxy: Manages network connectivity and maintains network rules across nodes. Implements the Kubernetes Service concept across every node in a given cluster.

# Etcd: 
* Etcd: Stores all cluster data. Consistent and highly available Kubernetes backing store. 

## Container-to-Container Networking 

<img src="https://sookocheff.com/post/kubernetes/understanding-kubernetes-networking-model/pod-veth-pairs.png" width="500" height="500" />


## Life of a packet: Pod-to-Pod, across Nodes

<img src="https://sookocheff.com/post/kubernetes/understanding-kubernetes-networking-model/pod-to-pod-different-nodes.gif" width="500" height="500" />



## How do you work with a Kubernetes cluster?

To work with a Kubernetes cluster, you must first determine its desired state. The desired state of a Kubernetes cluster defines many operational elements, including:

* Applications and workloads that should be running
* Images that these applications will need to use
* Resources that should be provided for these apps
* Quantity of needed replicas


To define a desired state, JSON or YAML files (called manifests) are used to specify the application type and the number of replicas needed to run the system.

Developers use the Kubernetes API to define a cluster’s desired state. This developer interaction uses the command line interface (kubectl) or leverages the API to directly interact with the cluster to manually set the desired state. The master node will then communicate the desired state to the worker nodes via the API.

Kubernetes automatically manages clusters to align with their desired state through the Kubernetes control plane. Responsibilities of a Kubernetes control plane include scheduling cluster activity and registering and responding to cluster events.

The Kubernetes control plane runs continuous control loops to ensure that the cluster’s actual state matches its desired state. For example, if you deploy an application to run with five replicas, and one of them crashes, the Kubernetes control plane will register this crash and deploy an additional replica so that the desired state of five replicas is maintained.


## Kubernetes Services

A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them. Services enable a loose coupling between dependent Pods. A Service is defined using YAML (preferred) or JSON, like all Kubernetes objects

# Three Types of Kubernetes Services

* ClusterIP (default) - Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.

* NodePort - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using   NodeIP:NodePort. Superset of ClusterIP.

* LoadBalancer - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. Superset of NodePort.

## Kubernetes VIP 

The Kubernetes VIP means that the IP is not attached to a network interface, technical (in the current default config with kube-proxy ) this means it's an IPtables entry, purely used to provide a stable communication endpoint.