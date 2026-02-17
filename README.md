# Basics Setup
---

# 🚀 Backend Stack Overview

* **Node.js** → JavaScript runtime
* **Express.js** → Web framework for Node
* **MongoDB** → NoSQL database
* **Postman** → API testing
* **GitHub** → Code hosting

---

# 📦 Project Initialization

```bash
npm init -y
```

Creates:

* `package.json`

Important fields:

```json
{
  "name": "project-name",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  }
}
```

---

# 📥 Install Dependencies

```bash
npm install express
npm install mongoose
npm install dotenv
npm install cors
npm install morgan
npm install bcryptjs
npm install jsonwebtoken
```

Dev dependency:

```bash
npm install -g nodemon
```

---

# 🗂 Basic Server Setup

### 📄 server.js

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello World");
});

const PORT = 5000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

Run server:

```bash
node server.js
```

Using nodemon:

```bash
nodemon server.js
```

---

# ⚙️ Useful Development Tools

* **Auto Import** → VS Code feature
* **Dotenv** → Manage environment variables
* **ESLint** → Shows JS errors/warnings
* **Prettier** → Code formatter
* **Material Icon Theme** → Folder icons
* **colors** → Colored console logs
* **morgan** → Logs API requests

---

# 🌍 Middleware

Middleware runs before request reaches controller.

```js
app.use(express.json());
app.use(cors());
app.use(morgan("dev"));
```

Custom middleware:

```js
app.use((req, res, next) => {
  console.log("Middleware running");
  next();
});
```

---

# 🏗 MVC Architecture (REST API)

### Structure

```
config/
models/
controllers/
routes/
middleware/
utils/
server.js
```

### Folders

* **models** → Database schemas
* **controllers** → Business logic
* **routes** → API endpoints
* **middleware** → Pre-processing functions
* **config** → Database setup
* **utils** → Helper functions

---

# 🗄 MongoDB Setup

### Cloud: MongoDB Atlas

* Create cluster
* Free tier ~512MB
* Allow IP: `0.0.0.0/0` (access from anywhere)

### Connection String contains:

* database name
* username
* password

---

# 📄 Database Configuration

### config/db.js

```js
const mongoose = require("mongoose");

const connectDB = async () => {
  await mongoose.connect(process.env.MONGO_URL);
  console.log("MongoDB Connected");
};

module.exports = connectDB;
```

In `server.js`:

```js
require("dotenv").config();
const connectDB = require("./config/db");

connectDB();
```

---

# 🔐 Password Hashing (bcrypt)

### Auto Salt Method

```js
bcrypt.hash(password, 10, (err, hash) => {});
```

### Manual Method

```js
bcrypt.genSalt(10, (err, salt) => {
  bcrypt.hash(password, salt, (err, hash) => {});
});
```

---

# 🔑 JWT Authentication

Install:

```bash
npm install jsonwebtoken
```

### Create Token

```js
const jwt = require("jsonwebtoken");

const token = jwt.sign(
  { id: user._id },
  process.env.JWT_SECRET,
  { expiresIn: "7d" }
);
```

### Verify Token (Middleware)

```js
jwt.verify(token, process.env.JWT_SECRET);
```

👉 Token is used to verify client identity.

---

# 🛣 Routes Example

```js
const express = require("express");
const router = express.Router();

router.delete(
  "/deleteUser/:id",
  authMiddleware,
  deleteUserController
);
```

---

# 🧠 Delete API Controller

```js
const deleteUser = async (req, res) => {
  await userModel.findByIdAndDelete(req.params.id);
  res.json({ message: "User Deleted" });
};
```

---

# 📮 Testing APIs

Use **Postman** to:

* Send GET
* POST
* PUT
* DELETE requests

---

# 🎯 REST API Flow

Client → Route → Middleware → Controller → Model → Database → Response

---

# 🧱 Express Server Production Pattern

```js
app.use("/api/v1/user", userRoutes);
```

---

# 🔥 Key Concepts to Remember

* Express handles routing
* Middleware runs before controller
* Controllers contain logic
* Models interact with DB
* JWT secures routes
* bcrypt protects passwords
* dotenv secures secrets
* MongoDB Atlas for cloud DB
* Nodemon for auto-restart

---

# 🧠 Backend Overview

## What is Backend?

Backend = Server + Business Logic + Database

Flow:

```
Browser / Mobile App
        ↓
      API
        ↓
    Backend Server
        ↓
     Database (DB)
```

Frontend sends request → Backend processes → DB stores/retrieves → Response sent back.

---

# 📁 Project Structure (Node + Express)

```
src/
│
├── index.js        → Entry point
├── config/         → DB & app configuration
├── models/         → Data schema
├── controllers/    → Business logic
├── routes/         → API endpoints
├── middleware/     → Request handlers
├── utils/          → Helper functions
├── constants/      → Enums, DB name, static values
```

---

## Folder Responsibilities

* **index.js** → Server start + DB connection
* **models** → Structure of data
* **controllers** → Functional logic
* **routes** → URL paths
* **middleware** → Runs before controller
* **utils** → Mail, token, helpers
* **config** → DB & environment setup

---

# 🚀 Server Setup (Express)

### Install

```bash
npm init -y
npm install express
```

---

### index.js

```js
import express from "express";

const app = express();

app.get("/", (req, res) => {
  res.send("Home Route");
});

app.listen(5000, () => {
  console.log("Server running");
});
```

---

# 📦 Important npm Commands

```bash
npm init -y         # Create package.json
npm install express # Install dependency
```

---

# 🌍 Environment Variables

Install dotenv:

```bash
npm install dotenv
```

Create `.env` file:

```
PORT=5000
MONGO_URL=your_db_url
```

Use in code:

```js
import dotenv from "dotenv";
dotenv.config();
```

---

# 🗃 Using ES Modules

In `package.json`:

```json
"type": "module"
```

Then use:

```js
import express from "express";
```

---

# 🔐 .gitignore

Used to hide:

* `.env`
* `node_modules`
* Private files

```bash
git init
touch .gitignore
```

---

# 🌐 Deployment

Steps:

1. Push code to GitHub
2. Use cloud platform (e.g., DigitalOcean, Render, Railway)
3. Configure environment variables
4. Connect to cloud database

---

# 🔗 API Routes

```js
app.get("/", (req, res) => {
  res.send("Home");
});
```

* `/` → Home route
* Defines path for API

---

# 📡 Frontend Integration

Frontend created using:

```bash
npm create vite@latest
```

Install Axios:

```bash
npm install axios
```

Axios → Used to send HTTP requests.

---

# 🔁 Proxy Configuration (Vite)

To avoid CORS in development:

### vite.config.js

```js
server: {
  proxy: {
    "/api": "http://localhost:5000"
  }
}
```

---

# 🗂 dist Folder

* Created after build
* Contains optimized production files

---

# 🧰 Common Backend Tools

* **Express** → Server framework
* **MongoDB** → Database
* **dotenv** → Manage secrets
* **Axios** → Frontend API calls
* **Git** → Version control
* **Cloud hosting** → Deployment

---

# 🧩 Basic Deployment Flow

Local Computer
↓
Node + Express running
↓
Push to GitHub
↓
Deploy to cloud server
↓
Connect to cloud DB

---

# 🎯 Backend Development Checklist

✔ Setup project
✔ Install dependencies
✔ Configure DB
✔ Create routes
✔ Add controllers
✔ Add middleware
✔ Use environment variables
✔ Secure with .gitignore
✔ Push to GitHub
✔ Deploy

---
