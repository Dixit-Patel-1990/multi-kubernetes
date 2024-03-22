
# Kubernetes Projects

# What we need

    1. Docker desktop for macOS M2
    2. Enable Kubernetes engine inside docker desktop
    3. Minicube for all other OS to manage VMs
    4. Kubectl is used to manage contianers inside VMs




To run single container inside Pod and expose it to outside world using kubernetes we need to create two types of objects (Pod and Service)/(Deployment and Service)

    1. Pod 
        - It's the smallest possible unit in kubernetes that we can deploy.
        - After creating pod object type we can only change image nothing else.
           - For example: in client-pod.yaml file we can only update the name of the image but
             if we try to change the port from 3000 to anything else it will throw an error. 
             To address this issue we need new object type that is deployment

    2. Service
        - Nodeport
            To expose the container to outside world.(Usually used for development purposes)
        - ClusterIP
            Exposes the set of pods to other objects in the cluster
        - LoadBalancer
            Legacy way of getting traffic in to the cluster
        - Ingress
            Exposes a set of service to the outside world

    3. Deployment
        - Deployment is used to maintain the set of identicle pods and it makes sure that 
          the configuration is correct and pods are always in runnable state and right number 
          of pods exists. so basically itmonitors the state of each pod and updates it when 
          necessary.
          
    4. Secret
        - Secretly stores the information in the cluster such as the database password
        - kubectl create secret generic <secret_name> --from-literal key=value

            secret = type of object we are going to create
            generic / docker-registry / tls = type of secret
            <secret_name> = name of the secret that we are going to use later in config files
            --from-literal =  we are going to add secret information into this command, 
                              as opposed to from files



### Commands

To apply entire k8s directory 

```cmd
kubectl apply -f <directory-name>

kubectl apply -f k8s
```

To delete entire k8s directory 

```cmd
kubectl delete -f <directory-name>

kubectl delete -f k8s
```

To apply client-pod.yaml 

```cmd
kubectl apply -f <file-path>

kubectl apply -f client-pod.yaml
```

To apply client-node-port.yaml

```cmd
kubectl apply -f client-node-port.yaml
```
To apply client-deployment.yaml

```cmd
kubectl apply -f client-deployment.yaml
```

To get the information about the running objects. In this command we can also use service or any other object type.

```cmd
kubectl get Pods
```
To get detailed information about objects

```cmd
kubectl describe <object-type> <object-name>

kubectl describe pod client-pod
```

To delete the running object type
```cmd
kubectl delete -f <file-path>

kubectl delete -f client-pod.yaml
```

# multi-container-application

[Application Architecture](https://drive.google.com/file/d/1Gt0x9W6KQs3XwjJDoFcGXZFcnZ_m_GHW/view?usp=sharing)

This project is an extension to the multi client docker project. Here in this project we are creating 3 replicas for client and server containers.

In this project we will be creating individual files for each object types and subtypes.

From architecture image, we will be creating following files

    1. Deployment object file for multi-client
    2. Deployment object file for multi-server
    3. Deployment object file for multi-worker
    4. Deployment object file for redis
    5. Deployment object file for postgres

    6. clusterIP service for multi-client
    7. clusterIP service for multi-server
    8. clusterIP service for redis
    9. clusterIP service for postgres

    10. postgres persistent volume claim for postgres

    11. Ingress service to route outside traffic to multi-client and multi-server pods

Apart from this we also need nginx controller to route traffic from private subnet

    To install and delete ingress-nginx controller

    ```cmd
        kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
        kubectl delete deployment <deployment-name> -n <namespace>
        kubectl delete deployment ingress-nginx-controller -n ingress-nginx
    ```



## Authors
- [@Dixit Patel](https://github.com/Dixit-Patel-1990/Docker)