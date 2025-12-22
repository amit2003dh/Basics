
# Node.js & Express Commands (with Short Explanations)

---

## 1. Check Versions

```bash
node -v
npm -v
```

Checks installed Node.js and npm versions.

---

## 2. Initialize Node Project

```bash
npm init
```

Creates `package.json` with manual setup.

```bash
npm init -y
```

Creates `package.json` with default values.

---

## 3. Run Node Application

```bash
node index.js
```

Runs a Node.js file.

---

## 4. Install Dependencies

```bash
npm install package-name
```

Installs a package locally.

```bash
npm install express
```

Installs Express framework.

```bash
npm install mongoose
```

Installs MongoDB ODM.

---

## 5. Install Dev Dependencies

```bash
npm install nodemon --save-dev
```

Installs Nodemon for auto-restarting server during development.

---

## 6. Express Server Run

```bash
node server.js
```

Starts Express server manually.

```bash
npx nodemon server.js
```

Starts server with auto-reload.

---

## 7. Common Backend Libraries

```bash
npm install cors
```

Enables cross-origin requests.

```bash
npm install dotenv
```

Loads environment variables.

```bash
npm install jsonwebtoken
```

Used for authentication tokens.

```bash
npm install bcryptjs
```

Used for password hashing.

---

## 8. NPM Scripts

Example in `package.json`:

```json
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
}
```

Run scripts:

```bash
npm start
npm run dev
```

---

## 9. Remove / Update Packages

```bash
npm uninstall package-name
```

Removes a package.

```bash
npm update
```

Updates all packages.

---

## 10. Fix Dependency Issues

```bash
rm -rf node_modules package-lock.json
npm install
```

Reinstalls all dependencies.

---

## 11. Debug Mode

```bash
node --inspect server.js
```

Runs server in debug mode.

---

## 12. Git Commands (Backend)

```bash
git init
git add .
git commit -m "backend setup"
git push
```

Used for version control.

---

## 13. Production Process (Optional)

```bash
npm install pm2 -g
```

Installs PM2 process manager.

```bash
pm2 start server.js
```

Runs server in production mode.

---

## Interview One-Line Summary

> “These commands are used to initialize, run, manage, and deploy Node.js and Express applications.”

---


