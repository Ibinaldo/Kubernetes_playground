# Assignment 6

1. Start an Nginx Pod and expose it, using the NodePort Service type

## Solution
- Look at the yaml definition for Nginx-pod in **nginx-pod.yaml** and create it using the command ```kubectl create -f nginx-pod.yaml```

- after creation you want to expose the pod using the NodePort serice type. You can do this by running the following command
