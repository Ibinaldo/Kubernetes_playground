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
