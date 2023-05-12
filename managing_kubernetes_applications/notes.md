# 5.1 Managing Pods
* As Pods are not typically started by themselves as naked Pods, there are no good ways to start just a Pod from the command line

* Pods can be started from a YAML manifest, using ```kubectl create -f mypod.yaml``` commands

* In the YAML file, the following items are needed:
  1. apiversion
  2. kind
  3. metadata
  4. spec

Note: The command `kubectl explain <resource_name>` can be used to list the fields for supported resources.

* **Kubectl get pods**: Shows currently running Pods
* **kubectl describe pod <pod_name>**: Shows details about a Pod.
* **kubectl get pods <pod_name> -o yaml**: Shows the YAML specification of the Pod as it is currently running in the Etcd cluster database.
* **kubectl delete pods <pod_name>**: Deletes a pod

# 5.2 Understanding Deployments
* Deployments are the standard for running applications.

* Pods are started through the deployment "template" specification

* Deployments are adding important scalability and availability features to the Pod
    -  Replication
    -  Update strategy

* Deployments are using labels to monitor the availability of a sufficient amount of Pods

* Many Kubernetes API Objects are using labels to connect to other objects.

* ReplicaSets monitor the Pod label to verify a sufficient amount of Pods is available.

* Labels are automatically set when starting deployments

* **kubectl label** can be used to manually set a label.

* labels can also be used to query. e.g. ```kubectl get all --selector app=cmd-nginx```

# 5.3 Running applications in Deployments
* Running applications in a deployment is the standard

* Do NOT run naked Pods! (you'll miss most important advantages of running Kubernetes e.g. scalability, upgrade policy etc)

* Use ```kubectl create -f myapp.yaml``` to run an application from a YAML file

* Use ```kubectl create deployment myapp --image=myapp``` to run an application from the command line.

# 5.4 Managing Namespaces
* Namespaces provide isolated environments in a kubernetes environments

* Using Namesspaces makes sense in environments with multiple teams or projects

* Namespaces can use resource quote to divide cluster resources between multiple users

* Names of resources need to be unique within specific Namespaces

* By default, a **default** namespace (where your kubernetes resources are created), and a **kube-system** namespace (for kubernetes system objects) exist.

* ```kubectl create ns``` will create a Namespace

* With **kubectl get**, use **--all-namespaces/-A** to show resources in all namespaces

* Use **-n mynamespace** to specify which Namespace you want to work in.

## 5.4.1 Understanding Context
* The context consists of the cluster name and namespace that the current user connects to.

* Context is set in the user settings: use **kubectl config get-contexts** to show current context.

* If multiple clusters are available to a kubernetes client, switching context is relevant

* if multiple namespaces exist within a cluster, switching namespaces is relevant

* To get namespaces using **kubectl**, you would run the command ```kubectl get ns```. This is equivalent to using the **kubens** package.

* To create your own namespace, you run the command ```kubectl create ns <namspace_name>```

* You can specify the namespace in your YAML file under metadata for some kubernetes objects.


# 5.5 Managing Application scalability
* **kubectl scale** allows you to modify the number of replicas for a current application. You apply this command to the deployment itself

* **kubectl edit** allows you to edit the current etcd configuration to modify the number of replicas for a current application. This command essentially opens up the YAML definition for this file which you can edit.

# 5.6 Managing Application updates and rollbacks
* Major changes to a deployment will have the deployment history updated

* While changing deployment history, a new ReplicaSet is created, while the old ReplicaSet is maintained with 0 pods in it.

* This makes it easy to undo a change

* Use ```kubectl rollout history``` for an overview of recent changes

* Use ```kubectl rollout undo``` to revert a change.

* Example: ```kubectl rollout undo deployment <name_of_deployment> --to-revision=<revision_number>```
