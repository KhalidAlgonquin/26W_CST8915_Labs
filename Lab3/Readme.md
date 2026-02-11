# Lab 3 - CST8915 Full-stack Cloud-native Development: Deploying the Algonquin Pet Store on Azure

**Student Name**: Khalid Amchat  
**Student ID**: 041125350   
**Semester**: Winter 2026  

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/La5FoGif4R4)

---

## Lab 3 Repositories
- **order-service:** https://github.com/KhalidAlgonquin/CST8915-lab2-order-service
- **product-service:** https://github.com/KhalidAlgonquin/CST8915-lab3-product-service-Python
- **store-front:** https://github.com/KhalidAlgonquin/CST8915-lab2-store-front
- **rabbitMQ:** https://github.com/KhalidAlgonquin/CST8915-lab2-RabbitMQ

---

## Reflection Questions

### 1) What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?
Unfortunately, I couldn’t configure and verify the environment variables through the GitHub Actions workflow because I was unable to deploy the store-front to Azure Static Web Apps. The deployment was blocked by an Azure Policy violation in my subscription (see attached screenshot). As a workaround, I deployed the store-front on an Azure VM instead and configured the required environment variables using a .env file on the VM.

<img width="846" height="697" alt="Screenshot policy violation" src="https://github.com/user-attachments/assets/9335fc25-b431-4ee3-b722-6dcfe9e5892c" />

### 2) How does deploying microservices on Azure Web App Service differ from running them locally?
Locally, I control everything directly (ports, localhost URLs, and starting each service manually), and the services can talk to each other using localhost or local network addresses. On Azure App Service, each microservice runs in a managed environment with its own public URL, and we  must rely on App Service configuration for variables like ports and connection strings. Troubleshooting also changes: instead of local console output only, we often use Azure logs to diagnose deployment issues.

### 3) Why is it important to use environment variables for configurations in a cloud environment?
In the cloud, parameters like service URLs, credentials, and connection strings change between environments (local, test, production) and can also change when resources are recreated. Environment variables allow to update configuration without changing code, which supports the 12-Factor App approach and makes deployments safer and faster. They also help keep keys and secrets out of the repository (no hard-coded passwords or keys), and make the same build portable across different Azure resources by only changing the settings.
