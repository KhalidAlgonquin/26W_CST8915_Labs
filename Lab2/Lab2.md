# Lab 2 - CST8915 Full-stack Cloud-native Development

**Student Name**: [Khalid Amchat]
**Student ID**: [041125350]
**Course**: CST8915 Full-stack Cloud-native Development
**Semester**: Winter 2026

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/-h-acIKpZ9w)

---

## Reflection Questions

### What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?

The hard-coded settings were removed and moved to environment variables using .env. For order-service, dotenv was used so the app can load values like PORT and RABBITMQ_CONNECTION_STRING from the environment. For product-service, the PORT was read from the environment instead of hard-coding it. Since I deployed everything on 4 Azure VMs, I updated the .env files to use the public IP addresses of the other VMs (RabbitMQ IP for the order service, and order/product IPs for the store-front). For Backing Services, RabbitMQ ran on its own VM and the order-service connected to it using the connection string env variable, which matches the idea that backing services are external resources.

### Why is it important to use environment variables instead of hard-coding configurations in your application?

Because when you move from local to Azure VMs, things like IP addresses, ports, and credentials can change. With environment variables, I can update the .env file (like switching from localhost to a VM public IP) without changing the code. It’s also safer because you don’t want to push credentials or server addresses into GitHub, and it makes deployments easier to manage.

### Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?

Because each service is independent and can be built and deployed on its own VM. With separate repos, I can update or redeploy only one service (like order-service) without touching product-service or store-front. This keeps the project organized, reduces conflicts, and helps scalability because each service can grow or change at its own speed with its own dependencies and deployment process.
