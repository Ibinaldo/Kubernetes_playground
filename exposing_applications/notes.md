# 6.1 Understanding Kubernetes Networking
* By default, pods have internal I.P addresses

* Service object in Kubernetes is connected to the deployment using a label. It distributes the workload to the different pods, essentially acting as a LoadBalancer

* Ingress object is for http and https traffic only. It can be used to provide URL access to a service object. It can also be connected to multiple service objects (not very common)

# 6.2 Networking within a Pod
* Containers run within pods, the pods are the managed entities and these entities need to be reachable. Containers don't need IP address, the pod needs the IP address.

# 6.3 Managing services
* Service objects connect to deployments using labels.

* Service object needs to connect to pods. How?
  1. IP address: How the service object is going to be reachable
  2. Target Port: The port at which the service object will address the pods
  3. Endpoints: IP addresses of the pods themselves

* On physical nodes there is **kube-proxy**, which communicates to IP tables and creates forwarding rules to communicate to the endpoint IP addresses. It is a component that runs on all of the physical nodes.

## 6.3.1 Understanding Service Types
- ClusterIP: the default type; provides internal access only. Your Service will get IP address that's in the Cluster IP address range.

- NodePort: allocates a specific node port which needs to be opened on the firewall.

- LoadBalancer: Currently only implemented in public cloud. It will give you an external IP address, reachable by external users directly. It will Load Balance the workload between the different pods involved.

- ExternalName: a relatively new object that works on DNS names; redirection is happening at a DNS level

- Service without selector: Use for direct connections based on IP/port, without an endpoint. Useful for connections to database, or between namespaces. Less common

- To create a service, we use the command ```kubectl expose```

# 6.4 Using DNS in Kubernetes
- DNS is integrated in Kubernetes services automatically

# 6.5 Working with Ingress
* Ingress exposes HTTP and HTTPS routes to services running inside a cluster. Provides multiple benefits
  1. Services get externally reachable URLS
  2. Can load balance between different Services
  3. Ingress can take care of TLS/SSL termination

* Ingress needs an Ingress Controller to do the work.

* Ingress only exposes HTTP/HTTPS, other service types are explosed using the NodePort or LoadBalancer service type.
