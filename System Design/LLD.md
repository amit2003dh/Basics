# 🧠 Low Level Design (LLD) — 

LLD answers:
**“How exactly will we implement the system internally?”**

It focuses on:

* Classes
* Data models
* APIs
* Business logic
* Error handling
* Data structures
* Interactions between modules

Think of it as:
**Blueprint for developers.**

---

# 🆚 HLD vs LLD

| HLD                | LLD                     |
| ------------------ | ----------------------- |
| Big picture        | Detailed implementation |
| System components  | Classes & functions     |
| Architecture flow  | Code-level design       |
| Used by architects | Used by developers      |

---

# 🎯 Goals of LLD

1. Clear module boundaries
2. Clean class structure
3. Easy maintainability
4. Extensible system
5. Testable components

---

# 🏗 LLD Core Components

## 1️⃣ Class Design

Each entity becomes a class.

Example: E-commerce system

```
User
Product
Cart
Order
Payment
```

---

## 2️⃣ SOLID Principles (Must Know)

### S – Single Responsibility

One class → one responsibility

### O – Open/Closed

Open for extension, closed for modification

### L – Liskov Substitution

Child class must replace parent without breaking

### I – Interface Segregation

Small, specific interfaces

### D – Dependency Inversion

Depend on abstraction, not concrete class

---

# 📦 Example: LLD for E-Commerce System

---

## 1️⃣ User Class

Responsibilities:

* Store user info
* Manage cart

```java
class User {
    private String id;
    private String name;
    private Cart cart;

    public void addToCart(Product product) {}
}
```

---

## 2️⃣ Product Class

```java
class Product {
    private String id;
    private String name;
    private double price;
    private int stock;

    public boolean isAvailable() {}
}
```

---

## 3️⃣ Cart Class

```java
class Cart {
    private List<CartItem> items;

    public void addItem(Product p) {}
    public void removeItem(Product p) {}
    public double calculateTotal() {}
}
```

---

## 4️⃣ Order Class

```java
class Order {
    private String orderId;
    private User user;
    private List<CartItem> items;
    private OrderStatus status;

    public void placeOrder() {}
}
```

---

## 5️⃣ Payment Strategy (Design Pattern)

Use Strategy Pattern:

```java
interface PaymentMethod {
    void pay(double amount);
}
```

Implementations:

```java
class CreditCardPayment implements PaymentMethod {}
class UPIPayment implements PaymentMethod {}
```

Why?

* Open for extension
* Easy to add new payment types

---

# 🔄 Relationships

* User → Has Cart
* Cart → Has CartItems
* Order → Has Products
* Payment → Uses Strategy

---

# 📊 Data Modeling

Entities → Tables

User

* id (PK)
* name
* email

Product

* id (PK)
* price
* stock

Order

* id
* user_id (FK)
* total

---

# 🧱 Design Patterns Used in LLD

## 1️⃣ Singleton

Only one instance (e.g., DB connection)

## 2️⃣ Factory

Object creation logic separated

## 3️⃣ Strategy

Different behaviors (payment example)

## 4️⃣ Observer

Event-based updates (notifications)

---

# 🔒 Error Handling Design

* Use centralized exception handler
* Custom exceptions
* Logging layer

---

# 📡 API Design (LLD Perspective)

```
POST   /users
GET    /products
POST   /cart/add
POST   /order/place
```

Each route maps to:
Controller → Service → Repository → DB

---

# 🧩 Layered Architecture (LLD)

```
Controller Layer
Service Layer
Repository Layer
Database
```

---

## Controller

Handles HTTP requests

## Service

Business logic

## Repository

Database interaction

---

# ⚙ LLD Checklist

✔ Classes defined
✔ Relationships defined
✔ Interfaces defined
✔ Error handling
✔ DB schema
✔ API endpoints
✔ Edge cases handled
✔ Logging added
✔ Scalability considered

---

# 🧠 When Interviewer Says “Design X (LLD)”

You should:

1. Clarify requirements
2. Identify entities
3. Define classes
4. Add relationships
5. Apply SOLID
6. Add design patterns
7. Handle edge cases
8. Discuss extensibility

---

# 🚀 Advanced LLD Topics

* Thread safety
* Concurrency handling
* Rate limiting logic
* Caching layer design
* Memory optimization
* Event-driven design

---

# 🎯 Key Takeaway

LLD = Clean code structure + Object modeling + Design principles.

HLD decides:
👉 What components exist

LLD decides:
👉 How exactly they work internally

---
