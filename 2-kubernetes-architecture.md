### Overview

- orchestrator of microservises apps
- orchestrate == organise
- cluster: combination of multiple nodes
- <b>master nodes</b>: brains of cluster -  cluster's <b>control plane</b>
- <b>worker nodes</b>: do the work - reports back - watch for new instructions
- package application in containers
- wrap containers in pods
- for scaling and self healing: wrap containers in deployment 
- kubernetes YAML file: to define status of cluster: given to master


### Master node

- officially incharge of running the clusters
- should be always highly available: multimaster control planes required
- connect all master nodes with fast reliable networks
- one is better than two
- 3 is magic number:  choose odd numbers: to always have majority
- more than 5 master nodes can reach to consensus
- even number of master nodes can cause deadlocks : splitbrain
- kubernetes operates in active-passive multimaster model: only one master is ever actively making changes to the cluser: leader, others are followers
- modern version of one or more linux machines are reuired for master ndoes
- all masters run all master components and so as all the control plane services
- Hosted Kubernetes Model:  GKE, EKS, AKS: Performance, Availability, Updates, Api server flags are taken care by the cloud service providers
- good practice: not to run user or business applications of master nodes

### Components of Master node

1. API server (kube-apiserver)
   - front-end to the control plane
   - gateway to the cluster
   - communication between components of control plane is also done through apiserver
   - exposes to API (REST)
   - consumes JSON/YAML as manifest files
   - apiserver authenticates, authorizes and validates YAML manifest file
   - instructs other control plane components to deploy and manage as per the instructions from the manifests
  
2. Cluster Store (etcd)
   - Only persistent component of control plane
   - configs and state of the cluster as well as any apps running on it is stored
   - based on etcd - nosql database
   - performance is critical: gets more pressure in case of large databases
   - have recovery plans in case of failure
  
3. Kube-Controller-Manager
   - controller of controllers
   - contains
     1. Node controller
     2. Deployment controller
     3. Endpoints controller
  
   - watches bits of cluster in loop
   - reconciles if observed state is matching with desired state of the cluster

4. Kube-scheduler
   - Watches API servers for new work tasks and assigns them to the cluster nodes
   - also manages: affinity/anti-affinity, contraints, resources, taints


### Master Process
