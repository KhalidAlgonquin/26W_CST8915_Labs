# CST8915 Lab 8: Deploying Algonquin Pet Store to AKS

**Student Name**: Khalid Amchat  
**Student ID**: 041125350   
**Semester**: Winter 2026  

## Lab Objective
The goal of this lab was to deploy the **Algonquin Pet Store** microservices application to **Azure Kubernetes Service (AKS)**, configure the required services, and complete the two lab tasks:

1. Build and use my own Docker images for the application services.
2. Improve **MongoDB** and **RabbitMQ** by adding persistent storage and better high-availability support.

## Repository

GitHub repository link: https://github.com/KhalidAlgonquin/26W_CST8915_Lab8

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/eD12ZwZoCts)

---

## Services Used in This Lab
The following services were deployed to AKS:

- Store Front
- Store Admin
- Product Service
- Order Service
- Makeline Service
- AI Service
- MongoDB
- RabbitMQ

## Task 1: Use My Own Docker Images
For Task 1, I forked and cloned the required service repositories, built Docker images locally, pushed them to my own Docker Hub account, and updated the Kubernetes YAML file to use my custom images.

### Docker Images Used
- `khalidamc/store-front:lab8`
- `khalidamc/store-admin:lab8`
- `khalidamc/order-service:lab8`
- `khalidamc/product-service:lab8`
- `khalidamc/makeline-service:lab8`
- `khalidamc/ai-service:lab8`

## Task 2: Improve MongoDB and RabbitMQ
For Task 2, I updated the deployment to improve persistence and availability ([aps-all-in-one.yaml](aps-all-in-one.yaml)).

### MongoDB Changes
MongoDB was changed from a simple temporary deployment to a StatefulSet with persistent storage.

Changes applied:
- MongoDB runs with **3 replicas**.
- A **headless service** was used for stable pod DNS.
- Each replica gets its own **PersistentVolumeClaim (PVC)**.
- Data is stored in `/data/db`.

This allows MongoDB pods to restart without losing data.

### RabbitMQ Changes
RabbitMQ was also changed to use a StatefulSet with persistent storage.

Changes applied:
- RabbitMQ runs with a PVC (PersistentVolumeClaim) for persistent storage.
- The RabbitMQ data directory is mounted at `/var/lib/rabbitmq`.
- The enabled plugins file remains mounted from ConfigMap.

This setup allows RabbitMQ data to survive pod restarts.

---

## Deployment Steps
### 1. Connect to AKS
```bash
az aks get-credentials --resource-group lab8-cst8915-rg --name lab8-cluster --overwrite-existing
```

### 2. Apply ConfigMaps and Secrets
```bash
kubectl apply -f config-maps.yaml
kubectl apply -f secrets.yaml
```

### 3. Deploy the Application
```bash
kubectl apply -f aps-all-in-one.yaml
```

### 4. Verify Resources
```bash
kubectl get pods
kubectl get svc
kubectl get statefulset
kubectl get pvc
```

---

## Validation and Testing
### Application Access
After deployment, the following services were accessible:
- **Store Front** through a LoadBalancer service
- **Store Admin** through a LoadBalancer service

### MongoDB Persistence Test
To prove MongoDB persistence:
1. I created orders through the application.
2. I confirmed that the data appeared in the admin page.
3. I restarted a MongoDB pod.
4. After the pod restarted, the order data was still available.

Example command used:
```bash
kubectl delete pod mongodb-0
```

### RabbitMQ Persistence Test
To prove RabbitMQ persistence:
1. I accessed RabbitMQ Management UI.
2. I created a test durable queue with persistent messages.
3. I restarted the RabbitMQ pod.
4. I verified whether the queue still existed after restart.

Example command used:
```bash
kubectl delete pod rabbitmq-0
```
---

