### **What is Prop Drilling? (Simple Explanation)**

![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1621786299509/_smEdcGcm.png?utm_source=chatgpt.com)

![Image](https://media2.dev.to/dynamic/image/width%3D1000%2Cheight%3D420%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ftar15qb7qlyoq99cpsxh.jpg?utm_source=chatgpt.com)

**Prop drilling** is when **data is passed from a parent component to deeply nested child components through multiple intermediate components**, even when those middle components don’t need the data.

---

## Simple example (no code)

```
App
 ↓
Home
 ↓
Restaurant
 ↓
Menu
 ↓
FoodItem   ← needs the data
```

Data goes through **Home → Restaurant → Menu**,
but only **FoodItem** actually uses it.

👉 This unnecessary passing is **prop drilling**.

---

## Why prop drilling is a problem

* Makes code **hard to read**
* Components become **tightly coupled**
* Hard to maintain as app grows
* Small changes affect many files

---

## How to avoid prop drilling

* `useContext`
* Global state (Redux, Zustand)
* Component composition

---

## One-line interview answer

> “Prop drilling is passing props through multiple components that don’t need them just to reach a deeply nested component.”

---

## Project-based example (Food App)

> Passing `cart` from `App → Home → Menu → FoodItem` instead of using a global cart context.

---

## Fresher closing line

> “I avoid prop drilling by using Context for shared data like auth and cart.”


### **When prop drilling is actually OK ✅**

![Image](https://react.dev/_next/image?q=75\&url=%2Fimages%2Fdocs%2Fdiagrams%2Frender_tree.png\&w=1080\&utm_source=chatgpt.com)

![Image](https://miro.medium.com/1%2AhIFyNceKz3QEp1aLdKNI2g.png?utm_source=chatgpt.com)

Prop drilling is **not always bad**. It’s **perfectly fine** in these cases:

---

### 1️⃣ Small component trees

If the data passes through **1–2 levels only**, prop drilling keeps things **simple and explicit**.

> Example: `Parent → Child → Button`

---

### 2️⃣ Data is used by most components

If **almost every child needs the data**, passing props is clear and readable.

> Example: layout settings, UI flags

---

### 3️⃣ Components are tightly related

When components are **part of the same feature** and unlikely to be reused elsewhere.

> Example: a form and its input fields

---

### 4️⃣ Temporary or one-off data

For short-lived or feature-specific data, adding Context can be **overkill**.

---

### 5️⃣ Early-stage or prototype apps

During MVP or learning phase, clarity beats abstraction.

---

## When it’s NOT okay ❌

* Deep nesting (3+ levels)
* Data used by only one deep child
* Global data (auth, cart, theme)
* Frequent changes causing refactors

---

## Interview-safe closing line

> “Prop drilling is fine for shallow, feature-specific data, but for shared global state I use Context.”

This answer shows **judgment**, not dogma.
