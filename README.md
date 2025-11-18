# 🚀 TradePay — Microservices-Based E-commerce Payment System

TradePay is a scalable and modular **E-commerce microservices application** designed to simulate a real-world shopping and payment workflow. It demonstrates how modern systems manage product listings, handle orders, and process payments using **highly decoupled services** that communicate through REST APIs with **Feign clients**, registered via a **Service Registry** and secured using **API Gateway patterns**.

This project is ideal for understanding distributed systems, service discovery, fault tolerance, and reactive integrations in a Java microservices ecosystem.

---

## 🏗️ Architecture Overview

The system consists of four independently deployable microservices:

| Microservice             | Responsibility                                 |
|--------------------------|-----------------------------------------------|
| **Product Service**      | Manages product catalog and inventory         |
| **Order Service**        | Handles placement and tracking of orders      |
| **Payment Service**      | Processes payments and transaction status     |
| **Service Registry**     | Registers all services using Eureka Server    |
| **TradePay API Gateway** | Central entry point for all services using Eureka|

A single **API Gateway** routes requests to these services, and **Feign Clients** enable inter-service communication. **Resilience4j Circuit Breaker** is used to ensure fault tolerance between dependent services.

---

## 🛠️ Technologies Used

- **Java 17**
- **Spring Boot 3.x**
- **Spring Cloud Netflix Eureka** (Service Discovery)
- **Spring Cloud Gateway** (API Gateway)
- **Feign Clients** (Inter-service REST communication)
- **Resilience4j** (Circuit Breaker / Fault Tolerance)
- **H2 / MySQL** (Databases)
- **Maven** (Build and dependency management)

---

## 🔄 Service Communication Flow

- Clients hit the **API Gateway** to access services.
- Gateway resolves the target service via **Eureka**.
- Services communicate using **Feign Clients**.
- If a service is down or slow, the **Circuit Breaker** prevents cascading failures.

---

## 📦 Microservices

### 🛍️ Product Service
- Exposes endpoints to manage products
- CRUD operations on product data
- Communicates with Order Service

### 📝 Order Service
- Places orders based on available products
- Calls Payment Service to confirm payment
- Includes fallback when Payment Service is unavailable

### 💳 Payment Service
- Processes and verifies payments
- Simulates success and failure scenarios
- Handles circuit breaker logic

### 🔍 Service Registry
- Acts as a discovery hub using Spring Cloud Netflix Eureka
- All services register here for dynamic resolution

### 🌐 API Gateway
- A unified entry point for clients
- Routes to Product, Order, and Payment services
- Important for rate limiting, monitoring, and security

---

## 🧪 Circuit Breaker Demo

To test Resilience4j Circuit Breaker:
1. Stop the Payment Service.
2. Invoke an Order creation.
3. Observe fallback response in the Order Service.

---

## 📁 Directory Structure

The project is structured into the following core microservices:

```tree
TradePay/
├── product-service/
├── order-service/
├── payment-service/
├── service-registry/
└── api-gateway/
```
---

## ▶️ How to Run

### Prerequisites
- JDK 17+
- Maven 3.8+

### Steps
1. Clone the repo:
   ```bash
   git clone https://github.com/Mr-AB007/TradePay.git
   cd TradePay
   ```

2. Start Service Registry:
    ```bash
    cd service-registry
    mvn spring-boot:run
    cd ../product-service && mvn spring-boot:run
    cd ../order-service && mvn spring-boot:run
    cd ../payment-service && mvn spring-boot:run
    cd ../api-gateway
    mvn spring-boot:run
3. Check service registration at:
   👉 http://localhost:8761

---
### 🌟 Features

- Fully modular and scalable microservices
- Dynamic service discovery via Eureka
- Fault-tolerant communication using Circuit Breaker
- RESTful endpoints orchestrated via API Gateway
- Simple project structure ideal for learning microservices
---
