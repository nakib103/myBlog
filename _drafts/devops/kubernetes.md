---
layout: post
title: "Kubernetes"
category: jekyll update
---

> Kubernetes is portable, extensible, and open source platform for managing containerized workload and services that facilitates both declarative configuration and automation.

### Configuration

- local/playground
  - minikube

- production
  - kubeadm
  - TKGi
  - GKS
  - AWS EKS

### Components
![need_update kubernetes components]({{ site.base_url }}/_images/kubernetes_components.png)

#### Control Plane
Control Plane components make global decision about the cluster as well as detects and responds to different cluster events.

##### kube-apiserver
kube-apiserver exposes the Kubernetes API and front end of the Control Plane. It scales horizontally that is by making more instances.

##### etcd
etcd is a key-value store that keeps all cluster data.

##### kube-scheduler
kube-scheduler watches for newly created pods that are not assigned to any node yet. It selects the node to run the pod factoring the individual and collective resource requirements, hardware/software/policy constraints, affinity/anti-affinity specifications, data locality, inter-workload interference, and deadlines.

##### kube-controller-manager
kube-controller-manager runs controller process like node controller, job controller, endpoint controller etc. Each controller is a separate process but kube-controller-manager compiles them into single binary and run as single process. 

##### cloud-controller-manager
Similar to kube-controller-manager cloud-controller-manager runs controller process that links Kubernetes cluster with cloud provider API.

#### Node
Node components run in each pod maintaining running pods and Kubernetes runtime environment.

##### kubelet
kubelet takes a set of PodSpecs and ensure that container described on those PodSpecs are maintained and healthy.

##### kube-proxy
kube-proxy manages network rules and helps implement Services resources. kube-proxy uses your clusters packet filtering layer if there is one otherwise it sends/receives packet itself.

##### container runtime
Container runtime is responsibel running the container such as docker, containerd, CRI-O.

#### Addons
Addons uses Kubernetes resource to implement different cluster features. The namespaced addon resource resides in kube-system namespace. Some addons are - 

##### DNS
Cluster DNS is mandatory and all Kubernetes clusters have it.

##### Web UI
minikube dashboard minikube dashboard
in other cases (such as TKGi)

{% highlight bash %}
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.2.0/aio/deploy/recommended.yaml
{% endhighlight %}

##### Container-resource Monitoring
##### Cluster-level Logging

### Kubernetes API
Kubernetes API is exposed by kube-apiserver and is an HTTP Rest API that lets user, different parts of the cluster and external components to communicate with each other.

There are different way to communicate with Kubernetes API server -

- Using direct REST calls
We will need to provide the api server location and credential to the http client (wget, curl). One of the way to do is running kubectl in proxy mode. 
{% highlight bash %}
kubectl proxy --port=8080 &
curl http://localhost:8080/api
{% endhighlight %}
- CLI tools like kubectlor kubeadm
- Client libraries 

### Kubernetes Objects
Kubernetes objects are persistent entities that define the cluster state. When we create a Kubernetes objects Kubernetes tries to keep the object. To create, delete, or modify a Kubernetes object we need to request to Kubernetes API describing the object in JSON. Another simple way to do it is write the description in .yaml and use kubectl to make the request to Kubernetes API.

#### Object Description
The .yaml description must include these 4 fields - 

- apiVersion : which version of Kubernetes API will be used to create the object
- kind : the type of object
- metadata : name , namespace , UID, labels, annotations like information
- spec : the desired state of the object
- status : these field is not defined by user rather it is defined by Kubernetes system

We describe the desired state of the object in spec field of the object description and the Kubernetes Control Plane try to maintain the state and record current states in status.

#### Object Management
We can use kubectl in 3 ways to manage (create, delete, update) objects - 

- imperative command: single line kubectl commands - 
{% highlight bash %}
kubectl create deployments nginx --image nginx
{% endhighlight %}
- imperative object declaration: object description inside a file (.yaml or .json) and run command using kubectl -
{% highlight bash %}
kubectl apply -f nginx.yaml
{% endhighlight %}
- declarative object declaration: keep the object configuration files (.yaml or .json) inside a directory and run kubectl command on the directory - 
{% highlight bash %}
kubectl apply -f <directory>
{% endhighlight %}

#### Object Terms
##### Namespace
Namespace are virtual cluster inside a physical cluster. Every clusters starts with 4 namespaces - 

- default - namespace for resource with no namespace
- kube-public - resides resource readable by all users even those who are not authorized
- kube-system - resides resource created by Kubernetes system
- kube-node-lease - resides lease resource associated with each node

Most of the resources are inside namespaces except few (like namespace themselves and low-level resource like node, persistentVolume). 
{% highlight bash %}
kubectl config set-context --current namespace=<namespace name>
{% endhighlight %}

##### Name
Each Kubernetes object of specific resource must have unique name within a namespace/cluster. e.g. - 

{% highlight yaml %}
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  ...
{% endhighlight %}

##### UID
Each Kubernetes object inside namespace/cluster must have unique UID

##### Labels and Selectors

- Labels
Labels are key/value pair that are attached to objects for identification purpose. Each keys must be unique for an object.

Syntax -
  - key: valid key can compose of 2 parts - a. prefix and b. name. Prefix is optional and if added must be a valid DNS subdomain. 
    - If prefix is not mentioned the label is assumed to be private to the user. 
    - Automated system component (kube-scheduler , kube-controller-manager etc.) , when adding labels, must specify prefix. 
    - kubernetes.io and k8s.io prefixes are reserved for Kubernetes.
  - value: only consist of name.

The taxonomy for key and value names -
  - must be 63 characters or less (value name can be empty),
  - unless empty, must begin and end with an alphanumeric character ([a-z0-9A-Z]),
  - could contain dashes (-), underscores (_), dots (.), and alphanumeric between.

e.g. - 
{% highlight yaml %}
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    environment: development
    app: nginx
{% endhighlight %}

- Selectors
Unlike name and UID labels are not unique. By using a label selector we can select a range of Kubernetes object. There are 2 types of selectors - 

  - equality based (requirements): = == != are used to match key and value of label. 
  {% highlight bash %}
  kubectl get pods -l envirenment=development,app!=apache
  {% endhighlight %}
  - set based (requirements): in notin exists are used to match keys to a set of values.
  {% highlight bash %} 
  kubectl get pods -l 'environment in (development, prod), !tier'
  {% endhighlight %}

  `,`: Multiple requirements can be separated by comma and it works as logical AND operator. But in set based requirements the comma that separates the value (development, prod) works as logical OR operator.

Uses
  - service and replicationcontroller uses selector to select other resources such as Pods to work on. They can use only map in object description file (json or yaml) and equality based requirement.
  - Job, Deployment, ReplicaSet, DaemonSet can use both equality and set based requirements - 
  ...
  {% highlight yaml %}
  spec:
  selector:
    matchLabels:
      environment: production
    matchExpressions:
      - {key: app, operator: notin, value: [apache, django]}
  {% endhighlight %}
  - pods can use nodeSelector selector to select on which nodes it should run based on node labels - 
  {% highlight yaml %}
  ...
  spec:
  ...
  nodeSelector:
    nodeLabel: value
  {% endhighlight %}

[Recommended Labels][kubernets recommended_labels] - 
Using app.kubernets.io prefixed labels to share common labels for resources.

##### Annotations

Annotations are similar to Labels in that they provide information to the Kubernetes object but unlike Labels they are not used for identification purpose.

Annotations are also key/value pair and their syntax is exactly same to that of Labels. e.g. - 
{% highlight yaml %}
apiVersion: v1
kind: Pod
metadata: 
  name: my-pod
  annotations: 
    someAnnotation: andItsValue
{% endhighlight %}

##### Field Selectors
Field selector like Label selector let us select Kubernetes objects based on some fields (the allowed fields vary by resource type but metadata.name and metadata.namespace are always allowed).
e.g. - 
{% highlight yaml %}
kubectl get pods --field-selector metadata.name=nginx
kubectl get pods --field-selector metadata.name=nginx,metadata.namespace!=default
kubectl get deployments,services --field-selector metadata.name=web
{% endhighlight %}
We can use = == != operator and , for multiple requirements.

### Nodes
#### Creating nodes
Node can be created in 2 ways - 
- kubelet on a node self-registers to control plane.
- user manually add node.
An example of yaml for node - 

{% highlight yaml %}
apiVersion: v1
kind: Node
metadata: 
  name: 107.109.211.64
  labels:
    name: my-node
{% endhighlight %}

After user creates a node - 
- Kubernetes creates a node object internally (run the above yaml - it will create a node object immediately)
- Kubernetes checks that the kubelet has registered to the API server that matches metadata.name
- Kubernetes checks if the node is healthy, otherwise it is barred from any cluster activity.

#### Node Registration
--register-node - if kubelet have this flag as true (default value) if will try to self register. To create node manually using kubectl set this flag to false.

Following are the options that kubelet configure when self registering -
- --kubeconfig - path to credential to authenticate itself against API server.
- --cloud-provider - how to talk to cloud provider
- --register-node - whether to self-register
- --register-with-taints - register node with taints (comma separated <key>:<value>:<effect>)
- --node-ip - ip address of the node
- --node-labels - labels for the node
- --node-status-update-frequency - frequency at which kubelet post NodeStatus to API.

#### Node Scheduling
Node can be made un-schedulable by following command - 
{% highlight bash %}
kubectl cordon <node name> 
{% endhighlight %}
To make it schedulable again - 
{% highlight bash %}
kubectl uncordon <node name>
{% endhighlight %}
- Un-schedulable node do not take further new pods.
- Pods that are part of DaemonSet can tolerate being run on un-schedulable node.

#### Node Status
We can see NodeStatus by running kubectl describe node <node name>. NodeStatus contain following information - 

##### Addresses
It varies with cloud provider or bare metal configuration - 
- Hostname - hostname of the node
- InternalIP - IP that accessible only within cluster
- ExternalIP - IP that externally routable. 

##### Conditions
Node can have following conditions - 

- Ready - True (if node is healthy and accepting pods), False (if node is not healthy and not accepting pods), and Unknown (if node monitor has not heard from node in last --node-monitor-grace-period which is 40 seconds)
- DiskPressure - True/False
- MemoryPressure - True/False
- PIDPressure - True/False
- NetworkUnavailable - True/False

##### Capacity
Describe resource available to a node - cpu, memory, storage, maximum number of pods.

##### Allocatable
Describe the amount of resource that is available to be consumed by normal podes

##### Info
General information of the nodes such kernel version, OS type & version, kubelet version, kube-proxy version etc. 

#### Node Controller
Node Controller is one of the controller that is managed by --kube-controller-manager in the Control Plane. It does the following - 

- assign CIDR block to node
- keep up to date the nodes that are in it’s list with cloud provider list of virtual machine. 
- monitor node healths.

#### Node Monitoring
##### Heartbeats
There are 2 types of heartbeats from kubelet to API server - 

- NodeStatus - kubelet sends NodeStatus every 5 minutes or earlier if there is a status change.
- Lease Object - Each node has associated Lease object in kube-node-lease namespace. kubelet create and update API server about Lease object at every 10 seconds.

#####   from Control Plane
kube-controller-manager - 

- checks and syncs NodeStatus at every --node-monitor-period which is 5 seconds.
- if heartbeats is not found NodeReady condition updated to ConditionUnknown.
- if NodeReady condition is False/Unknown for --node-monitor-grace-period which is 40 seconds the pods in the node are marked for eviction.
- the pods are deleted after --pod-eviction-timeout period which is 5 minutes.

Sometimes kubelet is out of communication with API server and the pod eviction decision cannot be sent to kubelet. In such case the pods in un-reachable nodes keep running until communication is established.

#### Control Plane - Node Communication
Kubernetes have a “hub-and-spoke“ way of communication. All API usage from node or pods terminate at API server.  None of the other control plane components are designed to communicate remotely.

##### Node - Control Plane
API server receives requests from nodes and pods over a secure HTTPs port with one or more form of client authentication enabled.
The other control plane components also communicate with API server over secure port.
Therefore the communication from node to API server can be run over a untrusted/public network.

##### Control Plane - Node
There are 2 ways of communication - 
- via kubelet : uses kubelet's HTTPs endpoint but does not authenticate.
- via kube-apiserver proxy: uses default HTTP endpoint so communication is not encrypted nor authenticated.

Therefore the communication from API server to node is not safe to be run over a untrusted/public network.
There is another communication option using Konnectivity which is replacing the previous SSH connection.

### Controllers
Control loop is a non-terminating loop that regulates the state of the system.

A Kubernetes controller -
- tracks at least one Kubernetes object to get it desired state from the spec of the object.
- tries to achieve the desired state by itself (Direct Control) or by other resource type (via API server). 

For example, a job controller - 
- get the desired state from the spec of the job description.
- creates one or more pods to run the tasks.

Kubernetes uses a lot of controllers and the built-in controllers are inside kube-controller-manager. We can also create controllers ourselves that run outside the control plane.

### Sources
https://kubernetes.io/docs/home/

[kubernets recommended_labels]: https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/