# Assignment
Create an Nginx application. Based on the application created, export the configuration into a file called **mynginx.yaml**

Solution
1. You can create an Nginx application using the minikube dashboard. In this example, we create it on the command line
2. Run the command ```kubectl get all``` to get a list of resources currently running in kubernetes. In my example I have a niginx deployment called **cmd-nginx**
3. To get the deployment details we follow the blue print: ```kubectl get <resource_type> <resource_name> -o yaml > <file_name>```
4. In my example, i'll run the command: ```kubectl get deployment cmd-nginx -o yaml > mynginx.yaml``
