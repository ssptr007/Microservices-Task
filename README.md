![image](https://github.com/user-attachments/assets/f0343d6f-7717-4b59-8ccc-acad6595ed78)# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

## Services and Endpoints

### **User Service**
- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**  
    ```
    curl http://localhost:3000/users
    ```
    Or open in your browser: [http://localhost:3000/users](http://localhost:3000/users)

---

### **Product Service**
- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**  
    ```
    curl http://localhost:3001/products
    ```
    Or open in your browser: [http://localhost:3001/products](http://localhost:3001/products)

---

### **Order Service**
- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**  
    ```
    curl http://localhost:3002/orders
    ```
    Or open in your browser: [http://localhost:3002/orders](http://localhost:3002/orders)

---

### **Gateway Service**
- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**  
    ```
    curl http://localhost:3003/api/users
    ```
  - **Products:**  
    ```
    curl http://localhost:3003/api/products
    ```
  - **Orders:**  
    ```
    curl http://localhost:3003/api/orders
    ```

---

## Instructions
1. Start all services using the `docker-compose` file:
   ```
   docker-compose up
   ```
2. Once the services are running, use the above endpoints to verify the functionality.

Happy testing!

---
Step 1: Dockerfile Creation

- **gateway-service/Dockerfile**

```
FROM node:22
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3003
CMD ["node","app.js"]
```
- **order-service/Dockerfile**

```
FROM node:22
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3002
CMD ["node","app.js"]

```
- **product-service/Dockerfile**

```
FROM node:22
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3001
CMD ["node","app.js"]
```
- **user-service/Dockerfile**

```
FROM node:22
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node","app.js"]
```

Step 2: Docker Compose Configuration
**docker-compose.yml**

```
version: '3.8'

services:
  user-service:
    build:
      context: /home/krishna/test/Microservices-Task/Microservices/user-service
    container_name: user-service
    ports:
      - "3000:3000"
    networks:
      - microservices-network

  product-service:
    build:
      context: /home/krishna/test/Microservices-Task/Microservices/product-service
    container_name: product-service
    ports:
      - "3001:3001"
    networks:
      - microservices-network

  order-service:
    build:
      context: /home/krishna/test/Microservices-Task/Microservices/order-service
    container_name: order-service
    ports:
      - "3002:3002"
    networks:
      - microservices-network

  gateway-service:
    build:
      context: /home/krishna/test/Microservices-Task/Microservices/gateway-service
    container_name: gateway-service
    ports:
      - "3003:3003"
    networks:
      - microservices-network
    depends_on:
      - user-service
      - product-service
      - order-service

networks:
  microservices-network:
    driver: bridge
```

Step 3: Local Testing & Validation

![image](https://github.com/user-attachments/assets/9d046458-5130-4a36-800b-aa6dfdc80427)

![image](https://github.com/user-attachments/assets/73afb27b-e682-485e-a1fc-a71892d94fe2)

![image](https://github.com/user-attachments/assets/abf6b748-803a-49c4-b7f3-6377eba305d4)

![image](https://github.com/user-attachments/assets/df6a8b16-34e3-4d72-a25f-d223e5373ce4)




