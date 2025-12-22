### **Why do we use CORS? (Simple, interview-ready explanation)**

![Image](https://docs.aws.amazon.com/images/sdk-for-javascript/v2/developer-guide/images/cors-overview.png?utm_source=chatgpt.com)

![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1599591569159/Ylc2deIBk.png?utm_source=chatgpt.com)

**CORS (Cross-Origin Resource Sharing)** is used to **allow or control requests between different origins** (different domain, port, or protocol).

---

## In simple words

> Browsers block requests to other servers for security.
> CORS tells the browser **which requests are allowed**.

---

## Why CORS is needed

Modern browsers follow the **Same-Origin Policy**:

* Frontend: `http://localhost:5173`
* Backend: `http://localhost:5000`

These are **different origins** → browser blocks the request by default.

CORS **fixes this safely**.

---

## What CORS actually does

* Allows frontend to call backend APIs
* Prevents unauthorized websites from accessing your server
* Controls which origins, methods, and headers are allowed

---

## In your food delivery project

> React frontend runs on one port, backend on another.
> CORS enables secure communication between them.

---

## One-line interview answer

> “CORS is used to allow secure communication between frontend and backend running on different origins.”

---

## Fresher confidence add-on

> “Without CORS, the browser blocks API requests even if the backend is working.”


