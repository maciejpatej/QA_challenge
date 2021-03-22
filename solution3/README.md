##Task 3
```
3.  Your company's data scientist just finished working on an application and
    they want the code to be deployed to the Kubernetes cluster that you are
    maintaining. They went ahead and wrote the Dockerfile and docker-compose file
    to give you an idea of how they want the tool to be deployed. Your task is
    to deploy it as scalable pods that can be accessed at the URL
    streaming.quickalgorithm.com. Please write the Kubernetes configuration
    files for the aforementioned codebase, specifying the assumptions that were
    taken during the process.
```
   
##Answer:

1. For the development purpose I have created Minikube with Docker driver on my local machine. In the production environment I would create a cluster from a cloud provider (e.g. use GKE on GCP).
2. I build images from developer's Dockerfiles and push them to the registry. In the production environment I would apply a kubectl secret and push the image to the private registry (e.g. self hosted Registry or gcr.io).
3. I created Kubernetes yaml's based on the Docker-compose file. To make things faster I use Kompose to create a base file for every deployment and service and clean them up a bit while adding important variables that might be missing.
    Yamls/resources created:
    - api-service
    - api-deployment
    - frontend-service
    - frontend-deployment
    Using Kompose already generates files pointing to the correct ports, which reduces the risk of human error.
4. I created kustomization.yaml to neatly start everything with one `kubectl apply -k .\<dir>\` command (Yes, I am using Windows, please send help).
5. I add a namespace.yaml to create the namespace for the streaming app
6. WIP on Ingress