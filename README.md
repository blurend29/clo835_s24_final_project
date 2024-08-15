
# Full-Stack Application Deployment and Management on Kubernetes

In this project, I deployed a full-stack application on a Kubernetes cluster, which includes a Node.js backend, a MongoDB database, and an Nginx frontend. I used Docker for containerization, Kubernetes for orchestration, ConfigMaps for environment management, and Persistent Volumes for data storage. This project provided me with hands-on experience in deploying, managing, and scaling a complete application on Kubernetes.

## Steps used to complete the assignment/project

**Step 1: Set up the Kubernetes environment**

Start a Kubernetes cluster using Minikube.

```bash
minikube start
```

**Step 2: Containerize the application**

*Backend*

Install Required Dependencies for the backend:

```bash
cd backend
npm init -y
npm install express mongoose body-parser
```

Build, tag and push the Docker image:

```bash
docker build -t junjun290/node-backend .
docker tag junjun290/node-backend junjun290/node-backend:latest
docker push junjun290/node-backend:latest
```

*Frontend*

Build, tag and push the Docker image:

```bash
cd frontend
docker build -t junjun290/nginx-frontend .
docker tag junjun290/nginx-frontend junjun290/nginx-frontend:latest
docker push junjun290/nginx-frontend:latest
```

**Step 3: Apply Kubernetes Manifests:**

```bash
kubectl apply -f kubernetes/mongo/mongo-pv.yaml
kubectl apply -f kubernetes/mongo/mongo-pvc.yaml 
kubectl apply -f kubernetes/mongo/mongo-deployment.yaml 
kubectl apply -f kubernetes/mongo/mongo-service.yaml 
kubectl apply -f kubernetes/backend/backend-deployment.yaml 
kubectl apply -f kubernetes/backend/backend-service.yaml 
kubectl apply -f kubernetes/frontend/frontend-deployment.yaml 
kubectl apply -f kubernetes/frontend/frontend-service.yaml 
kubectl apply -f kubernetes/configmap.yaml 
kubectl apply -f kubernetes/secret.yaml 
```

**Step 4: Application Management:**

Scale out nginx-frontend and node-backend deployments:

```bash
kubectl scale deployment/node-backend --replicas=3
kubectl scale deployment/nginx-frontend --replicas=3
```

Monitor nginx-frontend and node-backend deployments:

```bash
kubectl logs -f deployment/node-backend
kubectl logs -f deployment/nginx-frontend
```

Port forwarding:

```bash
kubectl port-forward svc/nginx-service 8081:80
kubectl port-forward svc/node-backend-service 3000:3000
kubectl port-forward svc/mongo-service 27017:27017
```

**Step 5: Testing and Validation:**

Access the frontend via http://localhost:8081

Access the backkend via http://localhost:3000

Send a POST request via Postman using the URL http://localhost:3000/items

Send a GET request via Postman using the URL http://localhost:3000/items to retrieve items. Also retrieve items by accessing http://localhost:3000/items using a web browser.

Connect to the mongoDB database mydatabase via MongoDB Compass using the URI mongodb://localhost:27017

---
