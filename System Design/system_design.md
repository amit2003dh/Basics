---

# 🏗 System Design – Core Concepts

## 🔹 Scalability

### 1️⃣ Vertical Scaling (Scale Up)

* Buy bigger machine (CPU, RAM increase)
* Simple to implement
* ❌ Hardware limit
* ❌ Single point of failure

---

### 2️⃣ Horizontal Scaling (Scale Out)

* Add more machines
* Requires load balancer
* ✅ Better fault tolerance
* ✅ Scales well as users grow
* ⚠ Data consistency challenges

---

# ⚖ Vertical vs Horizontal

| Horizontal             | Vertical                    |
| ---------------------- | --------------------------- |
| Needs load balancing   | No load balancer            |
| Fault tolerant         | Single point failure        |
| Uses RPC/network calls | Inter-process communication |
| Scales well            | Hardware limit              |
| Distributed            | Single machine              |

---

# 🔁 Load Balancing & Consistent Hashing

### Load Balancing

Distributes traffic across servers.

Servers:

```
S1
S2
S3
```

### Hash-based Routing

```
hash(requestID) % N → server
```

---

### Consistent Hashing

* Minimizes data reshuffling
* Used in distributed caching (Redis, DynamoDB)
* Useful when servers are added/removed

---

# 📊 System Requirements

## Functional Requirements

Defines:

* What system should do
* Observable features

Example:

* User authentication
* Payments
* Search
* Report generation

---

## Non-Functional Requirements (NFRs)

Defines how system should behave:

* Performance → speed & responsiveness
* Security
* Usability
* Reliability → stability & uptime
* Scalability
* Maintainability
* Portability

---

# 🔄 System Development Lifecycle

1. Analyze
2. Plan
3. Design
4. Develop
5. Implement
6. Maintain

---

# 🧠 High-Level Design (HLD)

Big-picture architecture.

```
Users
  ↓
CDN / Edge
  ↓
Load Balancer / API Gateway
  ↓
Auth Layer
  ↓
Application Services
  ↓
Database
  ↓
Logs & Metrics
  ↓
Queue & Workers
```

Focus:

* Scalability
* Reliability
* Performance

---

# 🧩 Low-Level Design (LLD)

* Class diagrams
* Modules
* Data structures
* Logic definition

Focus:

* Implementation
* Maintainability

---

# 🚀 System Optimization Factors

1. Scalability
2. Performance
3. Reliability
4. Security
5. Maintainability
6. Interoperability
7. Usability
8. Cost-effectiveness

---

# 🌐 HTTP vs HTTPS

* HTTPS = HTTP + SSL/TLS encryption
* Secure data transfer
* Prevents MITM attacks

Flow:

```
Client → Request → Server
Server → Response → Client
```

---

# 🔄 Data Transfer Methods

## 1️⃣ Polling

Client repeatedly asks server.

## 2️⃣ WebSockets

* Full-duplex communication
* Single TCP connection
* Used in chat, gaming, live updates

---

# 🧰 Backend Frameworks

## Server-Side

* Node.js → scalable network apps
* Express.js → minimal web framework
* Django → Python-based
* Spring Boot → Java enterprise apps
* Ruby on Rails → convention-based framework

---

## Client-Side

* React → component-based UI
* Angular → SPA framework
* Vue.js → progressive framework
* Svelte
* Bootstrap → responsive design

---

# 🗄 Database Systems

## Relational

* MySQL
* PostgreSQL

## NoSQL

* MongoDB → JSON-like, scalable

## Embedded

* SQLite → serverless, lightweight

---

# 📡 Communication Protocols & APIs

## REST

* Uses HTTP methods
* Stateless

## GraphQL

* Query language for APIs
* Reduces over-fetching

## WebSockets

* Real-time bidirectional communication

---

# 🛠 Development & DevOps Tools

* Postman → API testing
* Swagger → API documentation
* Docker → Containerization
* Kubernetes → Orchestration
* Git → Version control

---

# 📈 Capacity Planning

Estimate:

* QPS (queries per second)
* Storage requirements
* Bandwidth
* Peak load

---

# 🔒 Resiliency Techniques

* Rate Limiting
* Logging & Monitoring
* Pagination & Filtering
* Retry Mechanisms
* Circuit Breaker

---

# 🎯 Quick Revision Summary

* Scale Up = Vertical
* Scale Out = Horizontal
* ACID ≠ CAP
* HLD = Big picture
* LLD = Implementation details
* Load Balancer distributes traffic
* WebSockets = Real-time
* HTTPS = Secure HTTP
* NFR = Performance, reliability, scalability

---
