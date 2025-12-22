### **Hooks (Simple, Fresher-Friendly Explanation)**

![Image](https://repository-images.githubusercontent.com/196048036/5fae96d6-a1e5-43bc-8556-4ab9d83d4ff2?utm_source=chatgpt.com)

![Image](https://dmitripavlutin.com/85fa02ee6610f1e08b247ef2f967139c/react-useeffect-hook.svg?utm_source=chatgpt.com)

![Image](https://guide.sst.dev/assets/understanding-react-hooks/react-class-lifecycle-flochart.png?utm_source=chatgpt.com)

**Hooks** are special functions in **React** that let you **use state and other React features inside functional components**—without writing class components.

---

## Why Hooks exist

Before hooks:

* State + lifecycle → only in **class components**
  After hooks:
* Same power → **functional components**
* Cleaner, shorter, easier to reuse

---

## Most Important Hooks (Interview-safe)

### 1️⃣ `useState`

Used to **store and update data** in a component.

> Example use: cart items, login status, button clicks

**Idea:**
State changes → UI updates automatically

---

### 2️⃣ `useEffect`

Used to **run code when something happens**:

* Component loads
* State changes
* API calls

> Example use: fetch food list, load user data

**Idea:**
“Do this when X changes”

---

### 3️⃣ `useContext`

Used to **share data globally** without prop drilling.

> Example use: auth data, cart data

**Idea:**
One source → many components

---

## Why Hooks are important (say this)

> “Hooks make components simpler, reusable, and easier to manage.”

---

## One-line fresher definition

> “Hooks let functional components manage state, side effects, and shared data.”

