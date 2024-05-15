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
