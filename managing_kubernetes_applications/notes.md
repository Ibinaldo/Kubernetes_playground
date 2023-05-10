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
