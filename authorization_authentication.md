### **Authentication vs Authorization (Clear & Interview-Ready)**

---

## Authentication

**Authentication = Who are you?**

It verifies the **identity of the user**.

* Happens **first**
* Uses login credentials (username/password, OTP, biometrics)
* Result: user is **verified**

**Example**

* Logging in with email and password
* Receiving a JWT token after login

**One-liner**

> Authentication checks **who you are**.

---

## Authorization

**Authorization = What can you do?**

It checks **permissions and access rights**.

* Happens **after authentication**
* Uses roles or tokens
* Result: access is **allowed or denied**

**Example**

* Admin can delete users
* Normal user can place orders but not manage food items

**One-liner**

> Authorization checks **what you are allowed to do**.

---

## Key Differences (Quick Table)

| Feature  | Authentication    | Authorization            |
| -------- | ----------------- | ------------------------ |
| Question | Who are you?      | What can you access?     |
| Order    | First             | Second                   |
| Based on | Credentials       | Roles / Permissions      |
| Outcome  | Identity verified | Access granted or denied |

---

## Real-World Example (Food App)

* Login with email/password → **Authentication**
* Only admin can access admin panel → **Authorization**

---

## Interview Golden Line

> “Authentication verifies identity, authorization controls access.”


