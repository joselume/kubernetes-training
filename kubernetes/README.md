
To send to a file the execution of a kubectl command:
(Reference: https://kubernetes.io/docs/reference/kubectl/conventions/)
```
kubectl run redis --image=redis --dry-run=client -o yaml > pod.yaml
kubectl create deployment --image=nginx nginx --dry-run -o yaml
kubectl create deployment nginx --image=nginx--dry-run=client -o yaml > nginx-deployment.yaml
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
kubectl create namespace test-123 --dry-run -o yaml
```

Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379
```
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
```

# List existing pods
kubectl get pods

# Show pods with more information including the node information
kubectl get pods -o wide

# Describe pod
kubectl describe pod <pod name>

# Create pods

    # Create pod from an image
    kubectl run nginx --image=nginx

    # Create pod and expose it to a certain port
    kubectl run custom-nginx --image=nginx --port=8080

    # Create a pod from a yaml file
    kubectl apply -f pod.yaml

# Edit Pods
A Note on Editing Existing Pods
In any of the practical quizzes if you are asked to edit an existing POD, please note the following:

If you are given a pod definition file, edit that file and use it to create a new pod.

If you are not given a pod definition file, you may extract the definition to a file using the below command:
```
kubectl get pod <pod-name> -o yaml > pod-definition.yaml
```
Then edit the file to make the necessary changes, delete and re-create the pod.

Use the following command to 
```
kubectl edit pod <pod-name> 
```
command to edit pod properties. 

# Replication Controller

To keep the desired number of pod replicas up and running

For scaling up & down depending on the application load

- Replication controller: old version
- Replica Set: new technology

# Replica Set

It is necessary use `labels` in the selector because that is 
how you say the replicaset what pods should be replicated 

- Run a Replica Set:
```
kubectl create -f replicaset-definition.yml
```
- List existing replica sets:
```
kubectl get replicas
```
- Delete existing replica sets:
```
kubectl delete replicaset myapp-replicaset
```
Edit/Update existing replicaset, this command will show you the yaml for edition:
```
kubectl edit replicaset myapp-replicaset
```

- Replace an existing replicaset
```
  kubectl replace -f replicaset-definition.yml
```
or using scale command with -f file option
```
  kubectl scale --replicas=6 -f replicaset-definition.yml
```
or using scale command with replicaset name
```
  kubectl scale --replicas=6 replicaset myapp-replicaset
```
# Deployment

- Create deployment:
```
kubectl create -f deployment-definition.yml

or 

kubectl create deployment webapp --image=kodekloud/webapp-coler --replicas=3
```

- List deployments:
```
kubectl get deployments
```
# Namespaces

List the pods in a specific pod different that the current:
```
kubectl get pods --namespace=kube-system
```

Create a pod in a different namespace:
```
kubectl create -f pod-definition.yml --namespace=dev
```

Create Namespace from a yml file definition
```
kubectl create -f namespace-dev.yml
```

Create Namespace using only command
```
kubectl create namespace d
```
Get pods in all namespaces
kubectl get pods --all-namespaces
```
kubectl create namespace d
```
