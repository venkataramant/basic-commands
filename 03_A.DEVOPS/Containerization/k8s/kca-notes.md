
Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation

Virtualization allows better utilization of resources in a physical server and allows better scalability because an application can be added or updated easily

Containers are similar to VMs, but they have relaxed isolation properties to share the Operating System (OS) among the applications. Therefore, containers are considered lightweight. Similar to a VM, a container has its own filesystem, share of CPU, memory, process space, and more. As they are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions

Loosely coupled, distributed, elastic, liberated micro-services

dynamically – not a monolithic stack 

K8S is a framework to run distributed systems resiliently.
It takes care of scaling and failover for your application, provides deployment patterns

Kubernetes provides you with:

Service discovery and load balancing
Storage orchestration
Automated rollouts and rollbacks
Automatic bin packing 
Self-healing 
Secret and configuration management

Kubernetes provides the building blocks for building developer platforms, but preserves user choice and flexibility where it is important.

Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state

robust, resilient, and extensible


<https://kubernetes.io/docs/setup/production-environment/>
```python
print("pythoncode here")
```

# Production considerations
	Availability 
	Scale
	Security and access management

# **Options**:
	Serverless
	Managed control plane
	Managed worker nodes
	Integration
# Production control plane
	Choose deployment tools
	Manage certificates
	Configure load balancer for apiserver
	Create multiple control plane systems
	Span multiple zones
	Manage on-going features
# Production worker nodes
Production-quality workloads need to be resilient and anything they rely on needs to be resilient (such as CoreDNS).

	Configure nodes:
	Validate nodes
	Scale nodes
	Autoscale nodes
	Set up node health check
# Production user management
	Authentication
	Authorization
		Role-based access control (RBAC): 
			Lets you assign access to your cluster by allowing specific sets of permissions to authenticated users. Permissions can be assigned for a specific namespace (Role) or across the entire cluster (ClusterRole). Then using RoleBindings and ClusterRoleBindings, those permissions can be attached to particular users.
		Attribute-based access control (ABAC): 
			Lets you create policies based on resource attributes in the cluster and will allow or deny access based on those attributes. Each line of a policy file identifies versioning properties (apiVersion and kind) and a map of spec properties to match the subject (user or group), resource property, non-resource property (/version or /apis), and readonly. 

# Container Runtimes
*Dockershim has been removed from the Kubernetes project as of release 1.24*

*Kubernetes 1.28 requires that you use a runtime that conforms with the Container Runtime Interface (CRI).*

*FlexVolume was deprecated in the Kubernetes v1.23 release*

several common container runtimes with Kubernetes.

    containerd
    CRI-O
    Docker Engine
    Mirantis Container Runtime

Read <https://kubernetes.io/docs/setup/production-environment/container-runtimes/>
# prerequisites
	Forwarding IPv4 and letting iptables see bridged traffic
	cgroup drivers
		On Linux, control groups are used to constrain resources that are allocated to processes
		Two cgroup drivers available:
			cgroupfs (default)
			systemd
				When systemd is chosen as the init system for a Linux distribution, the init process generates and consumes a root control group (cgroup) and acts as a cgroup manager.
				To set systemd as the cgroup driver, edit the KubeletConfiguration option of cgroupDriver and set it to systemd. For example:
```yaml
					apiVersion: kubelet.config.k8s.io/v1beta1
					kind: KubeletConfiguration
					...
					cgroupDriver: systemd


```


**CRI Configuration**

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| containerd      | /etc/containerd/config.toml       | /run/containerd/containerd.sock  |
| CRI-O   | /etc/crio/crio.conf        | /var/run/crio/crio.sock     |
| cri-dockerd   | -       | /run/cri-dockerd.sock     |
| Mirantis Container Runtime   | cri-dockerd      | cri-docker.socket    |

--pod-infra-container-image

# Installing Kubernetes with deployment tools
# Bootstrapping clusters with kubeadm

# Installing Kubernetes with kOps
To easily install a Kubernetes cluster on AWS.
# Installing Kubernetes with Kubespray
To install a Kubernetes cluster hosted on GCE, Azure, OpenStack, AWS, vSphere, Equinix Metal (formerly Packet), Oracle Cloud Infrastructure (Experimental) or Baremetal with Kubespray.

Kubespray is a composition of Ansible playbooks, inventory, provisioning tools, and domain knowledge for generic OS/Kubernetes clusters configuration management tasks.

Kubespray provides a way to verify inter-pod connectivity and DNS resolve with Netchecker. Netchecker ensures the netchecker-agents pods can resolve DNS requests and ping each over within the default namespace. Those pods mimic similar behavior as the rest of the workloads and serve as cluster health indicators.

# 2.1 Overview

# Understanding Kubernetes objects

A Kubernetes object is a "record of intent"

Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster.

		What containerized applications are running (and on which nodes)
		The resources available to those applications
		The policies around how those applications behave, such as restart policies, upgrades, and fault-tolerance

# Object spec and status

Almost every Kubernetes object includes two nested object fields that govern the object's configuration: the object spec and the object status. For objects that have a spec, you have to set this when you create the object, providing a description of the characteristics you want the resource to have: its desired state.

The status describes the current state of the object, supplied and updated by the Kubernetes system and its components. The Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```
# Labels and Selectors
Labels are key/value pairs that are attached to objects.
Labels can be used to organize and to select subsets of objects. 
Non-identifying information should be recorded using annotations.

Valid label keys have two segments: an optional prefix and name, separated by a slash (/)

The kubernetes.io/ and k8s.io/ prefixes are reserved for Kubernetes core components.

# Label selectors
The label selector is the core grouping primitive in Kubernetes.
```bash
kubectl get pods -l environment=production,tier=frontend
kubectl get pods -l 'environment in (production),tier in (frontend)'
kubectl get pods -Lapp -Ltier -Lrole

kubectl label pods -l app=nginx tier=fe

```
*Job, Deployment, ReplicaSet, and DaemonSet* 
```yaml
selector:
  matchLabels:
    component: redis
  matchExpressions:
    - { key: tier, operator: In, values: [cache] }
    - { key: environment, operator: NotIn, values: [dev] }
```
Valid operators include In, NotIn, Exists, and DoesNotExist.

# Namespaces

In Kubernetes, namespaces provides a mechanism for isolating groups of resources within a single cluster.

Namespaces are a way to divide cluster resources between multiple users (via resource quota).

Four initial namespaces:
	*default*
	*kube-node-lease*
	*kube-public*
	*kube-system*

<service-name>.<namespace-name>.svc.cluster.local

If a container only uses <service-name>, it will resolve to the service which is local to a namespace. 

# Annotations
	Kubernetes annotations to attach arbitrary non-identifying metadata to objects.

	Valid annotation keys have two segments: an optional prefix and name, separated by a slash (/).

# Field Selectors

	Field selectors let you select Kubernetes objects based on the value of one or more resource fields. Here are some examples of field selector queries:

    metadata.name=my-service
    metadata.namespace!=default
    status.phase=Pending
```bash
kubectl get pods --field-selector status.phase=Running
```
# Finalizers

	Finalizers are namespaced keys that tell Kubernetes to wait until specific conditions are met before it fully deletes resources marked for deletion. Finalizers alert controllers to clean up resources the deleted object owned.

	metadata.finalizers
	metadata.deletionTimestamp
	a 202 status code (HTTP "Accepted")

	-- kubernetes.io/pv-protection

	Kubernetes also processes finalizers when it identifies owner references on a resource targeted for deletion.

# Owner references, labels, and finalizers

	metadata.ownerReferences
	ownerReferences.blockOwnerDeletion

In Kubernetes, some objects are owners of other objects. For example, a ReplicaSet is the owner of a set of Pods. These owned objects are dependents of their owner.

	Owner references in object specifications
			Dependent objects have a metadata.ownerReferences field that references their owner object. A valid owner reference consists of the object name and a UID within the same namespace as the dependent object. 

Like labels, owner references describe the relationships between objects in Kubernetes, but are used for a different purpose. When a controller manages objects like Pods, it uses labels to track changes to groups of related objects. For example, when a Job creates one or more Pods, the Job controller applies labels to those pods and tracks changes to any Pods in the cluster with the same label.

The Job controller also adds owner references to those Pods, pointing at the Job that created the Pods. If you delete the Job while these Pods are running, Kubernetes uses the owner references (not labels) to determine which Pods in the cluster need cleanup.


Kubernetes also adds finalizers to an owner resource when you use either foreground or orphan cascading deletion.

# Cluster Components
!["components"]('https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg')
	
	Control Plane Components
		kube-apiserver 
		etcd
		kube-scheduler 
		kube-controller-manager
			Node controller
		 	Job controller
			EndpointSlice controller
			ServiceAccount controller
		cloud-controller-manager 
			Node controller
			Route controller
			Service controller
	Node Components
		kubelet
		kube-proxy
			kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.
			maintains network rules on nodesdr
		Container runtime
	Addons
		Addons use Kubernetes resources (DaemonSet, Deployment, etc) to implement cluster features. Because these are providing cluster-level features, namespaced resources for addons belong within the kube-system namespace.
		DNS
	Web UI (Dashboard)
	Container Resource Monitoring
	Cluster-level Logging
	Network Plugins
		Network plugins are software components that implement the container network interface (CNI) specification.

# API Discovery
 /api
 /apis
 /apis/<group>/<version> -- /apis/rbac.authorization.k8s.io/v1alpha1

# API Extension
	Custom resources 
	Aggregation layer.

# 2.2 Cluster Architecture
	Nodes
	Communication between Nodes and the Control Plane
	Controllers
	Leases
	Cloud Controller Manager
	Cgroup v2
	CRI
	Garbage Collection
	Mixed Version Proxy

# Node
	Registration:
		The kubelet on a node self-registers to the control plane
			--register-node
			--kubeconfig
			--cloud-provider
			--register-with-taints
			--node-ip
			--node-labels
			--node-status-update-frequency

		Manually add a Node object
	Node authorization mode 
	NodeRestriction admission
# Node Status
	Addresses
	Conditions
	Capacity and Allocatable
	Info
# Node Heartbeats
	.status
	Lease Objects (kode-node-lease namespace)
# Node Controller
	Assigning a CIDR block to the node when it is registered
	Keeping the node controller's internal list of nodes up to date with the cloud provider's list of available machines
	Monitoring the nodes' health (every 5 seconds)
		Kube-controller-manager flags
			--node-monitor-period
			--node-eviction-rate
			--unhealthy-zone-threshold
			--large-cluster-size-threshold
			--secondary-node-eviction-rate
			
		.status 
			Ready=Unknown/False
		evit Pods (in Case of Unknown)
# Node topology
	TopoloyManager
# Graceful node shutdown
	GracefulNodeShutdown
	shutdownGracePeriod
	shutdownGracePeriodCriticalPods
	"NotReady" Condition on Staus
	"reason" --> "node is shutting down"
# Pod Priority based graceful node shutdown
	critial and non-critical
	priority
	shutdownGracePeriodByPodPriority (for kubelet)
	GracefulNodeShutdownBasedOnPodPriority (FeatureGate)
	graceful_shutdown_start_time_seconds
	graceful_shutdown_end_time_seconds

# Non-graceful node shutdown handling
	-  StatefulSet cannot create a new pod with the same name
	node.kubernetes.io/out-of-service (taint)
	NodeOutOfServiceVolumeDetachfeature(FeatureGate)
# Swap memory management
	NodeSwap (FeatureGate) /cgroup v2
	--fail-swap-on=false (kubelet)
```yaml
	memorySwap:
      swapBehavior: UnlimitedSwap/limitedSwap
```
# Communication between Nodes and the Control Plane
	Node to ControlPlane:
		The "kubernetes" service (in default namespace) is configured with a virtual IP address that is redirected (via kube-proxy) to the HTTPS endpoint on the API server.
	API server to kubelet:
		--kubelet-certificate-authority (kube-apiserver)
		Fetching logs for pods.
		Attaching (usually through kubectl) to running pods.
		Providing the kubelet's port-forwarding functionality.
	API server to nodes, pods, and services 
		hese connections are not currently safe to run over untrusted or public networks.
	SSH tunnel is deprecated and use konnectivity service.

	Konnectivity Service:
		Konnectivity Server in ControlPlane
		Konnectivity agent in node's network.
# controllers
	In robotics and automation, a control loop is a non-terminating loop that regulates the state of a system.
	Controller pattern
		A controller tracks at least one Kubernetes resource type. These objects have a spec field that represents the desired state.

		Control via API server
		Direct control

	Desired vs current state

	Design
	Ways of running controllers
		built-in controllers provide important core behaviors.

# Leases
	Distributed systems often have a need for leases, which provide a mechanism to lock shared resources and coordinate activity between members of a set. In Kubernetes, the lease concept is represented by Lease objects in the coordination.k8s.io API Group, which are used for system-critical capabilities such as node heartbeats and component-level leader election.

	Node heartbeats
	Workloads
		Your own workload can define its own use of Leases
	API server identity
		Starting in Kubernetes v1.26, each kube-apiserver uses the Lease API to publish its identity to the rest of the system.
	Leader election
		Kubernetes also uses Leases to ensure only one instance of a component is running at any given time. This is used by control plane components like kube-controller-manager and kube-scheduler in HA configurations, where only one instance of the component should be actively running while the other instances are on stand-by
# Controllers
 In robotics and automation, a control loop is a non-terminating loop that regulates the state of a system.
	In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state
# Cloud Controller Manager
	The cloud-controller-manager is a Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.
	The controllers inside the cloud controller manager include
		Node controller
		Route controller
		Service controller
	Authorization:
		Node controller
			The Node controller only works with Node objects. It requires full access to read and modify Node objects.
		Route controller
			The route controller listens to Node object creation and configures routes appropriately. It requires Get access to Node objects.
		Service controller

			The service controller watches for Service object create, update and delete events and then configures Endpoints for those Services appropriately (for EndpointSlices, the kube-controller-manager manages these on demand).

			To access Services, it requires list, and watch access. To update Services, it requires patch and update access.

			To set up Endpoints resources for the Services, it requires access to create, list, get, watch, and update.
		Others:
			v1/Event:

				create
				patch
				update

			v1/ServiceAccount:

				create
# cgroup v2
	On Linux, control groups constrain resources that are allocated to processes.

	The kubelet and the underlying container runtime need to interface with cgroups to enforce resource management for pods and containers which includes cpu/memory requests and limits for containerized workloads
	cgroup v2 offers several improvements over cgroup v1, such as the following:

    Single unified hierarchy design in API
    Safer sub-tree delegation to containers
    Newer features like Pressure Stall Information
    Enhanced resource allocation management and isolation across multiple resources
        Unified accounting for different types of memory allocations (network memory, kernel memory, etc)
        Accounting for non-immediate resource changes such as page cache write backs
```sh
stat -fc %T /sys/fs/cgroup/
```
# Container Runtime Interface (CRI)
	The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components.
	The kubelet acts as a client when connecting to the container runtime via gRPC. The runtime and image service endpoints have to be available in the container runtime, which can be configured separately within the kubelet by using the --image-service-endpoint

# Garbage Collection
	Garbage collection is a collective term for the various mechanisms Kubernetes uses to clean up cluster resources
	    Terminated pods
    Completed Jobs
    Objects without owner references
    Unused containers and container images
    Dynamically provisioned PersistentVolumes with a StorageClass reclaim policy of Delete
    Stale or expired CertificateSigningRequests (CSRs)
    Nodes deleted in the following scenarios:
        On a cloud when the cluster uses a cloud controller manager
        On-premises when the cluster uses an addon similar to a cloud controller manager
    Node Lease objects

Owners and de

# Mixed Version Proxy
	UnknownVersionInteroperabilityProxy FeatureGate

```bash
kube-apiserver \
--feature-gates=UnknownVersionInteroperabilityProxy=true \
-proxy-client-cert-file
--proxy-client-key-file
--requestheader-client-ca-file
--peer-ca-file

```

# 2.3 containers
	Each node in a Kubernetes cluster runs the containers that form the Pods assigned to that node. Containers in a Pod are co-located and co-scheduled to run on the same node.
	
	Containers are intended to be stateless and immutable: you should not change the code of a container that is already running. 

	Container images
	Container runtimes
		specify the RuntimeClass for a Pod to make sure that Kubernetes runs those containers using a particular container runtime.
	Container environment
		
		A filesystem, which is a combination of an image and one or more volumes.
		
		Information about the Container itself.
			hostname/gethostname()
			pod/Namespace Names are in ENV
			User defined ENV variables
		
		Information about other objects in the cluster
	Runtime-class
		Configure the CRI implementation on nodes
		Create the corresponding RuntimeClass resources
		Scheduling
		Pod Overhead
	Container Lifecycle Hooks
		The hooks enable Containers to be aware of events in their management lifecycle and run code implemented in a handler when the corresponding lifecycle hook is executed

		PostStart
			FailedPostStartHook
			FailedPreStopHook
		PreStop

		Implementation Types:
			Exec
			HTTP
		Hook delivery guarantees
			at least once
		


# 2.4 Workloads
	A workload is an application running on Kubernetes. Whether your workload is a single component or several that work together, on Kubernetes you run it inside a set of pods.

	Deployment and ReplicaSet (ReplicationController)
	StatefulSet (each Pod with a PersistentVolume.)
	DaemonSet 
		a plugin to run cluster networking
	Job and CronJob 
		 a Job to define a task that runs to completion, just once
		 a CronJob to run the same Job multiple times according a schedule
---------------------------------------------------------------------------	
	# Pods
		Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
		The shared context of a Pod is a set of Linux namespaces, cgroups, and potentially other facets of isolation - the same things that isolate a container. 

		initContainers
			restartPolicy: Always
		appContainers
			.spec.os.name
		SidecarContainers featureGate
	# Pod templates
	# Pod update and replacement
		Most of the metadata about a Pod is immutable
		Allowed ones:
		spec.containers[*].image,
		spec.initContainers[*].image,
		spec.activeDeadlineSeconds
		spec.tolerations [Add new ones]
	# Resource sharing and communication
		Storage in Pods
		Pod networking (localhost/semaphores)
		Privileged mode for containers
	# Container probes
		ExecAction
		TCPSocketAction
		HTTPGetAction

	# Static Pods
		Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them
		The main use for static Pods is to run a self-hosted control plane

		The kubelet automatically tries to create a mirror Pod on the Kubernetes API server for each static Pod
	# Pod Lifecycle (PodStatus)
		Pending/Running
		Succeeded/Failed
		Unknown
		Status:
			set of Pod conditions
	# Container states
		Waiting
		Running
		Terminated
	# Container restart policy
		.spec.restartPolicy
	# Pod conditions
		A Pod has a PodStatus, which has an array of PodConditions 
			type,status,lastProbeTime,lastTransisitionTime,reason,message
		types:

			PodScheduled
			PodReadyToStartContainers
			ContainersReady
			Initialized
			Ready
	# Pod readiness
	# Pod network readiness
		PodReadyToStartContainersCondition
	# Pod scheduling readiness
	# Container probes
		initialDelaySeconds
		failureThreshold periodSeconds
		Success/Failure/Unknown
		mechanisms:
			exec:
			grpc:
			httpGet:
			tcpSocket:
		types:
			livenessProbe
			readinessProbe
			startupProbe


	# Pod lifetime
	# Init Containers
		Must run to completion before the Pod can be ready.
		All of the app containers in a Pod can start in parallel
		.spec.initContainers
		.status.initContainerStatuses

		activeDeadlineSeconds

		SidecarContainers (FeatureGate)
	# Ephemeral Containers
		Ephemeral containers differ from other containers in that they lack guarantees for resources or execution, and they will never be automatically restarted, so they are not appropriate for building applications
	# QOS Classes via resource requests
		Guaranteed,Burstable and BestEffort
	# User Namespaces
	# Downward API
		The downward API allows containers to consume information about themselves or the cluster without using the Kubernetes client or API server.

		environment variables
		files in a downwardAPI volume
	
	# Workload Resources
-------------------------------------------------------------------
	# Deployments
		A Deployment provides declarative updates for Pods and ReplicaSets.
		Usages:
			Create a Deployment to rollout a ReplicaSet. 
			Declare the new state of the Pods 
			Rollback to an earlier Deployment revision 
			Scale up the Deployment to facilitate more load.
			Pause the rollout of a Deployment
			Use the status of the Deployment 
			Clean up older ReplicaSets 
		Pod-template-hash label

		Proportional scaling
			RollingUpdate Deployments support running multiple versions of an application at the same time. When you or an autoscaler scales a RollingUpdate Deployment that is in the middle of a rollout (either in progress or paused), the Deployment controller balances the additional replicas in the existing active ReplicaSets (ReplicaSets with Pods) in order to mitigate risk. This is called proportional scaling.
		Deployment status (kubectl rollout status return zero)
			type: Progressing
			status: "True"

			1. progressing (reason:  below)
				creates a new ReplicaSet.
				scaling up its newest ReplicaSet.
				scaling down its older ReplicaSet(s).
				New Pods become ready or available
			2. Complete
				All of the replicas Uptodate/available
				No old replicas for the Deployment are running.
			3. Failed (.spec.progressDeadlineSeconds))
				    Insufficient quota
					Readiness probe failures
					Image pull errors
					Insufficient permissions
					Limit ranges
					Application runtime misconfiguration
		Clean up Policy 
			.spec.revisionHistoryLimit(10)
		Canary Deployment
		Pod Template
			The .spec.template and .spec.selector are the only required fields of the .spec.
		Replicas
		Selector
		Strategy 
			.spec.strategy.type==Recreate/Rolling Update
		.spec.strategy.rollingUpdate.maxUnavailable
		.spec.strategy.rollingUpdate.maxSurge
		.spec.progressDeadlineSeconds
		.spec.minReadySeconds
		.spec.revisionHistoryLimit
		.spec.paused

------------------------------------------------------------------------------
	# ReplicaSet
		A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time.
		A ReplicaSet is linked to its Pods via the Pods' metadata.ownerReferences field
		ReplicaSets are the successors to ReplicationControllers.

		Pod Selector:
			In the ReplicaSet, .spec.template.metadata.labels must match spec.selector, or it will be rejected by the API.
		Delete RS:
			--cascade=orphan
		Pod deletion cost:
			controller.kubernetes.io/pod-deletion-cost 
		
		ReplicaSet as a Horizontal Pod Autoscaler Target
------------------------------------------------------------------------------
	# StatefulSets
		StatefulSet is the workload API object used to manage stateful applications.Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.
		
		a StatefulSet maintains a sticky identity for each of its Pods. 

		StatefulSets are valuable for applications that require one or more of the following.

			Stable, unique network identifiers.
			Stable, persistent storage.
			Ordered, graceful deployment and scaling.
			Ordered, automated rolling updates.
		Limitations:
			    The storage for a given Pod must either be provisioned by a PersistentVolume Provisioner based on the requested storage class, or pre-provisioned by an admin.

				Deleting and/or scaling a StatefulSet down will not delete the volumes associated with the StatefulSet. This is done to ensure data safety, which is generally more valuable than an automatic purge of all related StatefulSet resources.

				StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service.

				StatefulSets do not provide any guarantees on the termination of pods when a StatefulSet is deleted. To achieve ordered and graceful termination of the pods in the StatefulSet, it is possible to scale the StatefulSet down to 0 prior to deletion.
				
				When using Rolling Updates with the default Pod Management Policy (OrderedReady), it's possible to get into a broken state that requires manual intervention to repair.
		# .spec.volumeClaimTemplates - Volume Claim Templates
		# .spec.minReadySeconds
		# apps.kubernetes.io/pod-index
		# .spec.ordinals .spec.replicas
		# Stable Network ID
		# Stable Storage
		# Pod Name Label  statefulset.kubernetes.io/pod-name
		# pod.Spec.TerminationGracePeriodSeconds ! =0
		# .spec.podManagementPolicy (OrderedReady/Parallel)
		# .spec.updateStrategy (OnDelete/RollingUpdate)
		# .spec.minReadySeconds
		# .spec.updateStrategy.rollingUpdate.partition
		# .spec.updateStrategy.rollingUpdate.maxUnavailable
		# PersistentVolumeClaim retention
			whenDeleted : Delete/Retain
			whenScaled: Retain
------------------------------------------------------------------------------
	# Daemonset
		A DaemonSet ensures that all (or some) Nodes run a copy of a Pod
		Some typical uses of a DaemonSet are:

			running a cluster storage daemon on every node
			running a logs collection daemon on every node
			running a node monitoring daemon on every node		
		# .spec.template.spec.nodeSelector or .spec.template.spec.affinity
		# .spec.template.spec.schedulerName
		# How Daemon Pods are scheduled
			A DaemonSet ensures that all eligible nodes run a copy of a Pod. The DaemonSet controller creates a Pod for each eligible node and adds the spec.affinity.nodeAffinity field of the Pod to match the target host. After the Pod is created, the default scheduler typically takes over and then binds the Pod to the target host by setting the .spec.nodeName field. If the new Pod cannot fit on the node, the default scheduler may preempt (evict) some of the existing Pods based on the priority of the new Pod.	
```yaml
nodeAffinity:
  requiredDuringSchedulingIgnoredDuringExecution:
    nodeSelectorTerms:
    - matchFields:
      - key: metadata.name
        operator: In
        values:
        - target-host-name
```
		Taints and tolerations:
			node.kubernetes.io/not-ready:NoExecute
			node.kubernetes.io/unreachable:NoExecute
			node.kubernetes.io/disk-pressure:NoSchedule
			node.kubernetes.io/memory-pressure:NoSchedule
			node.kubernetes.io/pid-pressure:NoSchedule
			node.kubernetes.io/unschedulable:NoSchedule
			node.kubernetes.io/network-unavailable:NoSchedule
		Communicating with Daemon Pods:
			push
			NodeIP and Known Port
			DNS
			Service
		Updating a DaemonSet
	Alternatives to DaemonSet
		Init scripts
		Bare Pods
		Static Pods

------------------------------------------------------------------------------
	# Jobs

	A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. 
		# .spec.parallelism
		# .spec.completions
		# .spec.completionMode
			NonIndexed
			Indexed

		# .spec.template.spec.restartPolicy = "OnFailure"/Never
	# Pod failure policy (featuregate)
	# Job termination and cleanup
------------------------------------------------------------------------------
	# CronJobs
		A CronJob creates Jobs on a repeating schedule.

		# .spec.schedule
		# .spec.jobTemplate
		# .spec.startingDeadlineSeconds
		# .spec.suspend
		# .spec.concurrencyPolicy (Allow/Forbid/Replace)
------------------------------------------------------------------------------
	# ReplicationController

	# .spec.template
# 2.5 Services, LoadBalancing and Networking
# 2.6 Storage
# 2.7 Configuration
# 2.8 Storage
# 2.9 Policies
# 2.10 Scheduling Preemption and Eviction
#

# TLS Subject  values
<https://kubernetes.io/docs/setup/best-practices/certificates/>

CN=**kubernetes-admin.system:masters** /O=**system:masters** 

	admin.conf  
		Subject: O = system:masters, CN = kubernetes-admin.system:masters
	admin.conf	default-admin	kubernetes-admin	system:masters

CN=**system:node:<nodeName>** /O=**system:nodes**

	kubelet.conf	default-auth	system:node:<nodeName> (see note)	system:nodes

CN=**system:kube-controller-manager**

	controller-manager.conf	default-controller-manager system:kube-controller-manager	

CN=**system:kube-scheduler**

	scheduler.conf	default-scheduler	system:kube-scheduler

# Running Node Conformance Test

	# $CONFIG_DIR is the pod manifest path of your Kubelet.
	# $LOG_DIR is the test output path.
	sudo docker run -it --rm --privileged --net=host \
	-v /:/rootfs -v $CONFIG_DIR:$CONFIG_DIR -v $LOG_DIR:/var/result \
	registry.k8s.io/node-test:0.2

	sudo docker run -it --rm --privileged --net=host \
	-v /:/rootfs:ro -v $CONFIG_DIR:$CONFIG_DIR -v $LOG_DIR:/var/result \
	-e FOCUS=MirrorPod \ # Only run MirrorPod test
	registry.k8s.io/node-test:0.2

	sudo docker run -it --rm --privileged --net=host \
	-v /:/rootfs:ro -v $CONFIG_DIR:$CONFIG_DIR -v $LOG_DIR:/var/result \
	-e SKIP=MirrorPod \ # Run all conformance tests but skip MirrorPod test
	registry.k8s.io/node-test:0.2

# POD Security
	alternatives for enforcing security profiles are being developed in the Kubernetes ecosystem:

    Kubewarden.
    Kyverno.
    OPA Gatekeeper.

# HA topology
<https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/>
# Installing kubeadm
    kubeadm: 
		the command to bootstrap the cluster.
    kubelet: 
		the component that runs on all of the machines in your cluster and does things like starting pods and containers.
    kubectl: 
		the command line util to talk to your cluster.

	sudo kubeadm reset
	kubeadm kubeconfig user 

Calico, Canal, and Flannel CNI providers are verified to support HostPort.
--pod-network-cidr 
--cri-socket
--control-plane-endpoint (cluster-endpoint to point to the address of your load-balancer in an high availability scenario.)
--apiserver-advertise-address=<ip-address>
--apiserver-advertise-address=2001:db8::101 (IPv6)
--kubernetes-version
--certificate-key
--resolv-conf
--hostname-override
--container-runtime-endpoint
--cri-socket
--upload-certs
	 the certificates of the primary control plane are encrypted and uploaded in the kubeadm-certs Secret.
# Binary Paths
kubeadm	 /usr/bin/kubeadm
kubelet	 /usr/bin/kubelet binary.
kubectl	/usr/bin/kubectl binary.
cri-tools	 /usr/bin/crictl binary.
kubernetes-cni	 /opt/cni/bin

