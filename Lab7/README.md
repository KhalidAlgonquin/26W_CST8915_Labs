# Lab 7: CST8915 Full-stack Cloud-native Development: Introduction to Kubernetes Basics

**Student Name**: Khalid Amchat  
**Student ID**: 041125350   
**Semester**: Winter 2026  

## Lab Objective

The objective of this lab is to deploy the Algonquin Pet Store application to Azure Kubernetes Service (AKS), to explore the foundational concepts of Kubernetes, focusing on using kubectl for basic operations, understanding the structure of Kubernetes YAML configuration files, and creating essential Kubernetes resources such as Pods, Deployments, and Services.

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/rAsVOk63RNU)

## Reflection Questions:

### 1- Is RabbitMQ stateless or stateful?
RabbitMQ need to be a stateful application because it manages queues, messages, bindings, and broker metadata. These are important runtime data that should survive pod restarts in a production environment.

### 2- Current issue in the provided deployment
In the provided YAML, RabbitMQ is deployed as a regular deployment, but no persistent volume is attached to it.
This means that RabbitMQ stores its data in ephemeral container storage. If the RabbitMQ pod is deleted, restarted, or rescheduled, its stored state may be lost (stateless).

### 3- What happens when the RabbitMQ pod is deleted or restarted?
Since RabbitMQ is managed by a Kubernetes Deployment, Kubernetes automatically recreates the pod after deletion. However, because there is no persistent storage, the new pod may start with empty local storage, which can cause loss of RabbitMQ data. This makes the deployment unsuitable for production use because message broker data should normally survive pod restarts or failures.

### 4- Possible Solutions
1. Use persistent storage: 
Attach a PersistentVolumeClaim to RabbitMQ so that the broker data is stored on persistent disk instead of temporary container storage. (https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
2. Use a StatefulSet: 
Replace the Deployment with a StatefulSet, which is better suited for stateful applications that need stable identity and persistent storage. (https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
3. Use a managed messaging service: 
A managed service such as Azure Service Bus can reduce the operational complexity of hosting and maintaining RabbitMQ inside Kubernetes.(https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)

### 5- Does Azure Service Bus solve the problem?
Azure Service Bus can solve the storage-management issue because it is a managed messaging service with durable messaging features.

## Notes about Setup Challenges

One setup challenge I faced was accessing the RabbitMQ Management Console through the Store-front external IP address. The `/products` endpoint was working correctly, which showed that the application and reverse proxy were partially functioning, but `/rabbitmq/` initially returned an `Object Not Found` error. The issue was caused by a path mismatch between the Store-front reverse proxy route and the RabbitMQ Management Console base path. I resolved this by adding the following environment variable to the RabbitMQ yaml configuration (like Lab6):

```yaml
- name: RABBITMQ_SERVER_ADDITIONAL_ERL_ARGS
  value: '-rabbitmq_management path_prefix "/rabbitmq"'

