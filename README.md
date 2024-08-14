
# Full-Stack Application Deployment and Management on Kubernetes

In this project, I deployed a full-stack application on a Kubernetes cluster, which includes a Node.js backend, a MongoDB database, and an Nginx frontend. I used Docker for containerization, Kubernetes for orchestration, ConfigMaps for environment management, and Persistent Volumes for data storage. This project provided me with hands-on experience in deploying, managing, and scaling a complete application on Kubernetes.

## Steps used to complete the assignment/project

**Build the docker image:**

```bash
docker build -t <dockerhub username>/time-service .
```

**Tag the docker image and push it to Docker Hub:**

```bash
docker tag <dockerhub username>/time-service <dockerhub username>/time-service:latest

docker push <dockerhub username>/time-service:latest
```

**Deploy the application by applying the Kubernetes manifests:**

```bash
kubectl apply -f deployment.yaml

kubectl apply -f service.yaml
```

**Run minikube tunnel to create a network route on my local machine to make Kubernetes LoadBalancer services accessible (Note: this is not needed if deploying the application in the cloud):**

```bash
minikube tunnel
```

**Check the status of the deployment and service:**

```bash
kubectl get deployments

kubectl get pods

kubectl get services
```

**Test the application:**

**Access the application using the external IP and the port.**

```bash
http://<external-ip>:3030
```

---
