
---

# 📝 Simple Article Platform (SAP) – Microservices Architecture

A **Java Spring Boot-based Article Publishing Platform** built using **microservices**, following **clean architecture** principles, with **service discovery** via Eureka and service communication with **OpenFeign**.

---

## ✅ Features

* 👥 **User Service** – Manage user registration & profiles
* 📝 **Post Service** – CRUD operations for blog articles
* 💬 **Comment Service** – Manage comments on posts
* 🔍 **Service Discovery** with Spring Cloud Eureka
* ⚡ Inter-service communication via **OpenFeign**
* 📦 Microservices architecture with **independent databases**
* 🧱 Clean project structure (Controller → Service → Repository → Entity/DTO)

---

## 🧩 Microservices Overview

| Microservice      | Responsibility             | Database  |
| ----------------- | -------------------------- | --------- |
| `user-service`    | User registration, profile | **MySQL** |
| `post-service`    | Blog posts CRUD            | **MySQL** |
| `comment-service` | Comments on posts          | **MySQL** |
| `eureka-server`   | Service discovery          | N/A       |

---

## 🧱 Tech Stack

* **Java 21**, Spring Boot **3.5.5**
* Spring Web, Spring Data JPA, Hibernate Validator
* Lombok, MapStruct
* Spring Boot Actuator
* Spring Cloud Netflix Eureka (Service Discovery)
* OpenFeign (Service-to-Service calls)
* **MySQL** (per service)

---

## 🗂️ Project Structure

```
sap-user-service/
sap-post-service/
sap-comment-service/
sap-eureka-server/
```

Each microservice:

```
src/
└── main/
    ├── java/com/sap/{service}/
    │   ├── config/
    │   ├── controller/
    │   ├── dto/
    │   ├── entity/
    │   ├── exception/
    │   ├── mapper/
    │   ├── repository/
    │   └── service/
    └── resources/
        ├── application.yml
```

---

## 📦 GitHub Repositories

| Microservice      | Repository Name     | Link                                                                    |
| ----------------- | ------------------- | ----------------------------------------------------------------------- |
| `user-service`    | SAP-User-Service    | [SAP-User-Service](https://github.com/CODERonak/SAP-User-Service)       |
| `post-service`    | SAP-Post-Service    | [SAP-Post-Service](https://github.com/CODERonak/SAP-Post-Service)       |
| `comment-service` | SAP-Comment-Service | [SAP-Comment-Service](https://github.com/CODERonak/SAP-Comment-Service) |
| `eureka-server`   | SAP-Eureka-Server   | [SAP-Eureka-Server](https://github.com/CODERonak/SAP-Eureka-Server)     |

---

## 👥 User Service

### Entity

```java
public class User {
    Long id;
    String username;
    String email;
    String passwordHash;
    String bio;
}
```

### Endpoints

| Method | Endpoint          | Description         |
| ------ | ----------------- | ------------------- |
| POST   | `/users/register` | Register a new user |
| GET    | `/users/{id}`     | Get user details    |
| PUT    | `/users/{id}`     | Update profile      |
| DELETE | `/users/{id}`     | Delete user         |

---

## 📝 Post Service

### Entity

```java
public class Post {
    Long id;
    Long authorId;     
    String title;
    String content;
}
```

### Endpoints

| Method | Endpoint      | Description                         |
| ------ | ------------- | ----------------------------------- |
| POST   | `/posts`      | Create post (validates user exists) |
| GET    | `/posts`      | List all posts                      |
| GET    | `/posts/{id}` | Get post with author info           |
| PUT    | `/posts/{id}` | Update post                         |
| DELETE | `/posts/{id}` | Delete post                         |

---

## 💬 Comment Service

### Entity

```java
public class Comment {
    Long id;
    Long postId;    
    Long userId;    
    String content;
}
```

### Endpoints

| Method | Endpoint              | Description                           |
| ------ | --------------------- | ------------------------------------- |
| POST   | `/comments`           | Create comment (validate user + post) |
| GET    | `/comments/post/{id}` | List comments for a post              |
| DELETE | `/comments/{id}`      | Delete comment                        |

---

## 🌐 Eureka Server

* All services (`user`, `post`, `comment`) register with **Eureka**
* Enables **service discovery** and dynamic service resolution

---

## 🔄 OpenFeign Communication

* Post Service → User Service (fetch author info)
* Comment Service → User Service (validate commenter)
* Comment Service → Post Service (validate post exists)

---

## ✅ Summary

* **User Service** → Manage users
* **Post Service** → Manage blog posts (depends on User Service)
* **Comment Service** → Manage comments (depends on User + Post Services)
* **Eureka Server** → Service discovery

---
