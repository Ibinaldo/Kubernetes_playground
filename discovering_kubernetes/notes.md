# 4.1 Working with **kubectl**

* The main tool you'll use when working with Kubernetes
```
kubectl -h  | less
```
command above provides help. Using the `-h` flag on commands provides help for specific commands e.g ```kubectl get -h | less``` for instance

You can create deployments, pods etc either via the command line or using YAML files.

# 4.2 Working with YAML files
- When an administrator just types commands to create resources in kubernetes, that is what is known as the **Imperative way**. It is not the Devops way of working since its difficult to reproduce.

- To guarantee reproducibility, YAML files are used to define resources. Also allows for version control

- Kubernetes resources are stored in the etcd database in JSON format

- JSON format is not easy to edit, which is why YAML is the current format to define Kubernetes resources

- Working with YAML files allows users to work the "DevOps way". When placed in Github repositories, version control is easy, and everybody will use the same code to create resources. This is the **Declarative way** of working with kubernetes.

- In YAML, relations between objects are defined by using indentation. Don't use tabs, but use spaces for indentation (usually 2 spaces).

- When working with YAML in kubernetes, API specification are followed.

- Very useful to look at the Kubernetes documentation, which has a lot of useful examples.

- After defining resources in YAML, you can use ```kubectl create -f myfile.yaml``` to create the resource, or ```kubectl delete -f myfile.yaml```to delete the resource.

- Pro Tip! YAML code can easily be generated using ```kubectl get <resources> -o yaml > myresource.yaml```

- Generally bad practice to create pod as stand alone resources since if you delete a pod, there is nothing in the kubernetes ecosystem that will create the resource again. Usually better to create **deployments** instead.


# 4.3 Core Kubernetes resources
- Kubernetes is all about managing pods. Pods can have one or more containers. Usually pods have one container.

- In a pod you can have volumes, which are making sure that files can be stored.

- Ideally, pods should be replicated for scalability and redundancy (server failures etc). In order to do this, Kubernetes makes use of the concept of **Replica sets**. These take care of the replication and is not something a user manages.

- The **deployment** is the application you create. It monitors the **Replica sets**, which in turn monitors the pods.

# 4.4 Kubernetes API
- The kubernetes API does not exist, its a collection of APIs which defines the resources that can be used in the kubernetes environment.

- ```kubectl api-resources``` shows a list of resources that is defined in the API. ```kubectl api-versions``` shows resource versions. ```kubectl explain <resource_name>``` allows users to explore attributes of kubernetes resources as they are defined in the API.
