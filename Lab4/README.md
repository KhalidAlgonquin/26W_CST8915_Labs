# Lab 4: CST8915 Full-stack Cloud-native Development: Introduction to Docker

**Student Name**: Khalid Amchat  
**Student ID**: 041125350   
**Semester**: Winter 2026  

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/7oL0eBHgXMA)

---

## Reflection Questions

### 1) What are the main differences between a Docker image and a Docker container?
A Docker image is a ready package that contains the app code and everything needed to run it. A Docker container is what you get when you start that image. The container is the running app, and it can create files and logs while it runs, but the image itself stays unchanged.

### 2) Explain how Docker's layered architecture improves efficiency.
Docker builds images in layers. When you rebuild an image, Docker can reuse layers that didn’t change (like the base image and installed dependencies). This makes builds faster and saves storage because the same layers can be shared across different images.

### 3) Why does each container get its own writable layer?
Each container gets its own writable layer so it can write data while running (like logs, temporary files, or cache) without changing the image. This also keeps containers isolated, so changes in one container don’t affect others.

### 4) What are the benefits of using Docker Compose over running containers individually?
Docker Compose lets us define all services (web app, database, Redis, etc.) in one file and start them with one command. It reduces manual setup, helps avoid mistakes, and makes it easier to manage networking, volumes, environment variables, and stopping/starting the whole application.
