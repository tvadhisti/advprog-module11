# Reflection Hello Minikube

1. The application logs before and after I exposed it as a Service.

- Screenshot 1:
![Screenshot 2024-05-14 at 14 57 07](https://github.com/tvadhisti/advprog-module11/assets/127074983/16b29e1d-2e93-4beb-9b7c-ab20dcde30f4)

- Screenshot 2:
![Screenshot 2024-05-14 at 14 54 41](https://github.com/tvadhisti/advprog-module11/assets/127074983/fd20bf4a-4dd9-4110-949f-0d33f497c25b)

Before I exposed my deployment as a service, the application logs were pretty basic, just showing messages like the app starting up its HTTP and UDP servers on ports 8080 and 8081. This just means that the app was up and running, but it wasn't interacting with anyone outside.

After I set up the service to expose my app, the logs started to show something new, entries for each HTTP GET request. This is a sign that people or systems from outside are now reaching my app. Each time I open the app while it’s exposed, the logs catch and record these visits. So, the more we access the app, the more entries we'll see in the logs, which reflects the increased activity.

2. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

The -n option in kubectl commands specifies the namespace in which to perform the operation. Namespaces in Kubernetes are used to organize and segregate groups of resources within the cluster.  We could have separate namespaces for development, testing, and production environments, ensuring that resources from one environment don't accidentally affect another.

If we don't use the -n option when running a kubectl command, Kubernetes automatically assumes we mean the "default" namespace. This "default" namespace is where Kubernetes looks for any resources we're trying to interact with unless told otherwise. But if we use -n, it shows us things from a special area reserved for Kubernetes' own use, which doesn't include our usual apps and services. Therefore, our user created deployments, pods, and services, which are in the default namespace, are not listed.

# Reflection on Rolling Update and Kubernetes Manifest File

1. The difference between Rolling Update and Recreate deployment strategy?
   
Rolling Update is a method where updates are implemented gradually, ensuring that the application remains accessible with minimal disruptions. It replaces old parts with new ones bit by bit. Rolling Update's gradual approach helps in seamlessly transitioning to newer versions while keeping the application running. In contrast, Recreate halts the current version entirely before launching the new one. This results in a downtime period during the update process. It's not the best choice if the app needs to be continuously available.

2. Deploying the Spring Petclinic REST using Recreate deployment strategy

- Create Deployment
![Screenshot 2024-05-15 at 21 15 47](https://github.com/tvadhisti/advprog-module11/assets/127074983/ca19822f-0129-43c0-a938-f8071cdc11cf)
This creates a Kubernetes deployment named spring-petclinic-rest

- Check pod and deployment status
![Screenshot 2024-05-15 at 21 17 19](https://github.com/tvadhisti/advprog-module11/assets/127074983/f38bd757-c6ef-4e1c-93b7-5ff3498aeb97)

- View Application Logs
![Screenshot 2024-05-15 at 21 18 51](https://github.com/tvadhisti/advprog-module11/assets/127074983/65a55d62-2d28-4c80-962a-efe01bd10513)
Ensure the application inside the pod is running correctly

- Expose Deployment as a Service
![Screenshot 2024-05-15 at 21 19 41](https://github.com/tvadhisti/advprog-module11/assets/127074983/f9225376-be75-4df3-8f99-dda907f0b661)

- Delete and Restart Minikube
![Screenshot 2024-05-15 at 21 20 42](https://github.com/tvadhisti/advprog-module11/assets/127074983/4db11576-83a3-4283-bb3b-1f218b409f5a)
These are used to reset Minikube, ensuring a clean state before testing.

- Modify Deployment Strategy to 'Recreate'
  
![Screenshot 2024-05-15 at 21 22 09](https://github.com/tvadhisti/advprog-module11/assets/127074983/7588e1de-02a8-4035-9a6b-48e08f77e44c)

Modify the deployment YAML file to change the strategy from the default (RollingUpdate) to 'Recreate'.

- Update Deployment Image
![Screenshot 2024-05-15 at 21 23 20](https://github.com/tvadhisti/advprog-module11/assets/127074983/f0cb3630-e1b3-4593-afa7-9168074cbb89)
Updates the deployment to use a new image version.

- Verify Updated Deployment
![Screenshot 2024-05-15 at 21 23 59](https://github.com/tvadhisti/advprog-module11/assets/127074983/b65cb287-0bec-451f-9a1e-c06e622f239d)
This test confirms that my Kubernetes environment handles pod recreation correctly under this deployment strategy.

3. Prepare different manifest files for executing Recreate deployment strategy.
The files for executing Recreate deployment strategy are deploy-recreate.yaml and service-recreate.yaml

4. Benefits of using Kubernetes manifest files? Recall my experience in deploying the app manually and compare it to my experience when deploying the same app by applying the manifest files (i.e., invoking `kubectl apply -f` command) to the cluster.

Using Kubernetes manifest files offers a handful of practical benefits that make managing applications much simpler. Firstly, these files allow me to set up my application's requirements in a way that Kubernetes understands and maintains automatically. This means once I define what I need, Kubernetes does the heavy lifting to keep everything running as expected. Plus, I can keep track of all our setup files just like I do with my code changes. This helps me see what changes were made, go back if I need to fix something, or see how things have changed over time. In terms of efficiency, using kubectl apply -f to apply these files is much faster and less error prone than typing out commands manually to set up each part of my application. 
