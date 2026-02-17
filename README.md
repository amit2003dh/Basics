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
