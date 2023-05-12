# Assignment

1. Create a YAML file that starts a deployment for nginx, using version 1.8 It should start 3 replicas and use the label **app=nginx**
2. Use the appropriate command to show all resources that use the label **app=nginx**
3. Change the number of replicas to 4
4. Upgrade the nginx deployment to the latest version of the image

## Solution
1. Deployment definition found in **nginx_lab4.yaml**. Then you run the command ```kubectl create -f nginx_lab4.yaml```.

2. Show all resources using the label **app=nginx** by running the command ```kubectl get all --selector app=nginx```

3. To change the number of replicas to 4, run the command  ```kubectl scale --replicas=4 deployment/nginx-lab-4```

4. To upgrade the latest nginx deployment, run the command ```kubectl edit deployment nginx-lab-4```. 
