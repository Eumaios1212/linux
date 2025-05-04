# Kubectl Commands with Examples for Beginners

Kubernetes is a tool for managing applications made up of many small containers (like mini-servers). `kubectl` is the command-line tool you use to talk to a Kubernetes cluster. This document lists common `kubectl` commands with beginner-friendly explanations and examples. Before using these commands, ensure `kubectl` is installed and configured with a kubeconfig file to connect to your Kubernetes cluster.

## Understanding Your Cluster

### View Cluster Information

Shows basic details about your Kubernetes cluster, like the addresses of its main components.

- **Why use it?** Helps you confirm that `kubectl` is connected to the right cluster.
- **Example:** Check if your cluster is up and running.
  
  ```bash
  kubectl cluster-info
  ```

### List All Contexts

Displays all the clusters and users you’ve set up in your kubeconfig file.

- **Why use it?** Useful to see which clusters you can switch between.
- **Example:** See all available clusters, like `minikube` or `prod-cluster`.
  
  ```bash
  kubectl config get-contexts
  ```

### Switch Context

Changes the cluster or user you’re working with.

- **Why use it?** Lets you switch between different clusters, like a local test cluster or a production one.
- **Example:** Switch to a cluster named `my-cluster`.
  
  ```bash
  kubectl config use-context my-cluster
  ```

## Managing Nodes

### List All Nodes

Shows all the machines (nodes) in your Kubernetes cluster.

- **Why use it?** Helps you see the computers running your applications.
- **Example:** Check the names and status of your cluster’s nodes.
  
  ```bash
  kubectl get nodes
  ```

### Describe a Node

Gives detailed information about a specific node, like its status and resources.

- **Why use it?** Useful for troubleshooting if a node isn’t working properly.
- **Example:** Get details about a node called `node-name`.
  
  ```bash
  kubectl describe node node-name
  ```

## Working with Namespaces

### List All Namespaces

Shows all namespaces in your cluster. Namespaces are like virtual folders to organize resources.

- **Why use it?** Helps you see how your cluster is organized.
- **Example:** List namespaces like `default`, `kube-system`, or `my-app`.
  
  ```bash
  kubectl get namespaces
  ```

### Create a Namespace

Creates a new namespace to group your resources.

- **Why use it?** Keeps your apps organized, like separating `dev` and `prod` environments.
- **Example:** Create a namespace called `my-namespace`.
  
  ```bash
  kubectl create namespace my-namespace
  ```

### Set Default Namespace

Sets a namespace as the default for your commands, so you don’t have to specify it every time.

- **Why use it?** Saves time when working in one namespace.
- **Example:** Make `my-namespace` the default for your current cluster.
  
  ```bash
  kubectl config set-context --current --namespace=my-namespace
  ```

## Managing Pods

### List All Pods

Shows all pods in the current namespace. Pods are the smallest units in Kubernetes, running one or more containers.

- **Why use it?** Lets you see the applications running in your cluster.
- **Example:** List pods like `web-app-123` or `database-456`.
  
  ```bash
  kubectl get pods
  ```

### Create a Pod

Creates a pod using a YAML file that describes its configuration.

- **Why use it?** This is how you start running an application in Kubernetes.
- **Example:** Create a pod from a file called `pod.yaml` (e.g., for a web server).
  
  ```bash
  kubectl apply -f pod.yaml
  ```

### Describe a Pod

Shows detailed information about a specific pod, like its status and events.

- **Why use it?** Helps you troubleshoot if a pod isn’t working as expected.
- **Example:** Get details about a pod named `pod-name`.
  
  ```bash
  kubectl describe pod pod-name
  ```

### Delete a Pod

Removes a specific pod from the cluster.

- **Why use it?** Cleans up pods you no longer need.
- **Example:** Delete a pod called `pod-name`.
  
  ```bash
  kubectl delete pod pod-name
  ```

### View Pod Logs

Displays the logs (output) from a pod’s container.

- **Why use it?** Helps you see what your application is doing or debug errors.
- **Example:** Check logs for a pod named `pod-name`.
  
  ```bash
  kubectl logs pod-name
  ```

### Execute a Command in a Pod

Opens a terminal inside a pod’s container to run commands.

- **Why use it?** Lets you interact directly with your application, like checking files or running tools.
- **Example:** Open a bash shell in a pod called `pod-name`.
  
  ```bash
  kubectl exec -it pod-name -- /bin/bash
  ```

## Managing Deployments

### List All Deployments

Shows all deployments in the current namespace. Deployments manage sets of pods to ensure they’re running correctly.

- **Why use it?** Helps you see the applications managed by Kubernetes.
- **Example:** List deployments like `web-app` or `api-server`.
  
  ```bash
  kubectl get deployments
  ```

### Create a Deployment

Creates a deployment using a YAML file that defines how many pods to run and their settings.

- **Why use it?** This is how you set up scalable, reliable applications.
- **Example:** Create a deployment from a file called `deployment.yaml`.
  
  ```bash
  kubectl apply -f deployment.yaml
  ```

### Scale a Deployment

Changes the number of pod replicas (copies) in a deployment.

- **Why use it?** Lets you scale your app up or down based on demand.
- **Example:** Scale a deployment called `my-deployment` to 3 pods.
  
  ```bash
  kubectl scale deployment my-deployment --replicas=3
  ```

### Rollout Status

Checks if a deployment update is complete and successful.

- **Why use it?** Ensures your app update went smoothly.
- **Example:** Monitor the rollout of `my-deployment`.
  
  ```bash
  kubectl rollout status deployment/my-deployment
  ```

### Rollback a Deployment

Reverts a deployment to its previous version if an update fails.

- **Why use it?** Fixes problems by going back to a working state.
- **Example:** Roll back `my-deployment` to the previous version.
  
  ```bash
  kubectl rollout undo deployment/my-deployment
  ```

## Managing Services

### List All Services

Shows all services in the current namespace. Services provide networking for pods, like load balancing.

- **Why use it?** Helps you see how your apps are accessible.
- **Example:** List services like `web-service` or `db-service`.
  
  ```bash
  kubectl get services
  ```

### Create a Service

Creates a service using a YAML file to define how pods are accessed.

- **Why use it?** Sets up networking for your application, like exposing a web server.
- **Example:** Create a service from a file called `service.yaml`.
  
  ```bash
  kubectl apply -f service.yaml
  ```

### Expose a Deployment as a Service

Creates a service to make a deployment accessible, like within the cluster or externally.

- **Why use it?** Quick way to expose your app without writing a YAML file.
- **Example:** Expose `my-deployment` on port 80 as a ClusterIP service (internal access only).
  
  ```bash
  kubectl expose deployment my-deployment --port=80 --type=ClusterIP
  ```

## Managing ConfigMaps and Secrets

### List All ConfigMaps

Shows all ConfigMaps in the current namespace. ConfigMaps store configuration data for your apps.

- **Why use it?** Helps you see the settings available to your pods.
- **Example:** List ConfigMaps like `app-config` or `db-settings`.
  
  ```bash
  kubectl get configmaps
  ```

### Create a ConfigMap

Creates a ConfigMap from a file or key-value pairs.

- **Why use it?** Lets your apps access configuration data, like database URLs.
- **Example:** Create a ConfigMap from a file called `config.properties`.
  
  ```bash
  kubectl create configmap my-config --from-file=config.properties
  ```

### List All Secrets

Shows all secrets in the current namespace. Secrets store sensitive data, like passwords.

- **Why use it?** Helps you manage secure information for your apps.
- **Example:** List secrets like `db-password` or `api-key`.
  
  ```bash
  kubectl get secrets
  ```

### Create a Secret

Creates a secret from key-value pairs or files.

- **Why use it?** Safely stores sensitive data for your apps.
- **Example:** Create a secret with a key `key1` and value `value1`.
  
  ```bash
  kubectl create secret generic my-secret --from-literal=key1=value1
  ```

## Monitoring Resources

### View Resource Usage

Shows how much CPU and memory your pods are using.

- **Why use it?** Helps you monitor performance and spot resource-heavy apps.
- **Example:** Check resource usage for all pods in the current namespace.
  
  ```bash
  kubectl top pods
  ```

### Apply a Resource

Creates or updates any Kubernetes resource (like a pod or deployment) from a YAML or JSON file.

- **Why use it?** This is the standard way to manage resources in Kubernetes.
- **Example:** Apply a configuration from a file called `resource.yaml`.
  
  ```bash
  kubectl apply -f resource.yaml
  ```

### Delete a Resource

Removes a resource defined in a YAML file or by name.

- **Why use it?** Cleans up resources you no longer need.
- **Example:** Delete a resource defined in `resource.yaml`.
  
  ```bash
  kubectl delete -f resource.yaml
  ```

## Debugging and Troubleshooting

### Get Events

Shows events in the current namespace, like pod creation or errors.

- **Why use it?** Helps you understand what’s happening in your cluster.
- **Example:** Check events to troubleshoot a failing pod.
  
  ```bash
  kubectl get events
  ```

### Port Forward to a Pod

Connects a local port on your computer to a port on a pod.

- **Why use it?** Lets you test or debug an app by accessing it locally.
- **Example:** Forward local port 8080 to port 80 on `pod-name`.
  
  ```bash
  kubectl port-forward pod-name 8080:80
  ```

### Describe a Resource

Gives detailed information about any Kubernetes resource, like a pod or service.

- **Why use it?** Great for debugging issues with any resource.
- **Example:** Get details about a resource (replace `<resource-type>` with `pod`, `service`, etc.).
  
  ```bash
  kubectl describe <resource-type> <resource-name>
  ```