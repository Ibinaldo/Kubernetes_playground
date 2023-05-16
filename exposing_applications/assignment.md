# Assignment 6

1. Start an Nginx Pod and expose it, using the NodePort Service type

## Solution
- Look at the yaml definition for Nginx-pod in **nginx-pod.yaml** and create it using the command ```kubectl create -f nginx-pod.yaml```. Make sure the pod has a label as a resource can not be exposed without a label. 

- After creation you want to expose the pod using the Node Port service type. You can do this by running the following command:

**kubectl expose pod nginx-pods-lab6 --type=NodePort --port=80 --dry-run=client -o yaml > nginx-lab6-svc.yaml**

- Then run the command to create the resource:  ```kubectl create -f nginx-lab6-svc.yaml```
