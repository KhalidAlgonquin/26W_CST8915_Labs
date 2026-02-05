# CST8915 Lab 1: Algonquin Pet Store on Azure VM

**Student Name**: Khalid Amchat

**Student ID**: 041125350

**Course**: CST8915 Full-stack Cloud-native Development

**Semester**: Winter 2026


---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/1XEv1IBIbF4)

---

## Technical Explanations

### Order Service (Node.js)

The Order Service is the backend service that handles customer orders. When the user places an order from the website, this service receives the request and starts the order workflow. It helps keep the order logic separate from the website UI, and the backend can handle orders in a more reliable way.

This service is built using Node.js, which is commonly used to create APIs because it handles web requests efficiently. In the microservices architecture, the Order Service focuses only on orders. The Store Front communicates with it through HTTP requests (when submitting an order). After receiving an order, the Order Service publishes a message to RabbitMQ, which acts as a message broker so orders can be processed without blocking the website.

### Product Service (Rust)

The Product Service is responsible for product information, such as the product list and product details. The Store Front depends on this service to display items in the shop. If the Product Service is not running, the website cannot show the catalog correctly because it has nowhere to fetch product data from.

This service is implemented in Rust, which is known for performance and safety. In the microservices architecture, it represents the products domain and exposes endpoints that other parts of the system can call. The Store Front interacts with the Product Service using HTTP requests to load the product catalog and display product details.

### Store Front (Vue.js)

The Store Front is the web user interface that customers open in their browser. It shows the product catalog and images, and it provides the forms needed to place an order. Its main job is to display the application to the user and send requests to backend services based on user actions.

It is built using Vue.js, a front-end framework that helps build interactive web pages using components. In the microservices design, the Store Front acts as the client that connects to multiple backend services. It calls the Product Service to load and display products, and it calls the Order Service when the user submits an order. The Store Front does not connect to RabbitMQ directly; RabbitMQ communication is handled by the Order Service.


---

## Acknowledgments

Lab1 repository instructions, lab 1 Video Tutorial, Azure documentation, and course notes.
