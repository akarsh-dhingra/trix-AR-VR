# 🍕 Blog 3 — Building the Web AR Menu (Foundation Phase)

**Author:** Srishti Garg  
**Date:** March 29, 2026  

---

## 📌 Introduction

In the previous stages, the base structure of the AR Menu was already developed, including UI elements like dish navigation, ingredient panels, and layout.

However, the system was incomplete because it lacked:

- 3D visualization  
- AR interaction  
- QR-based access  

This phase focuses on converting the static menu into a functional web-based system.

---

## 🧠 Understanding the System (Very Important)

Before coding, it is important to understand where everything happens:

### 1. GitHub (Code Storage)

All project files (HTML, JavaScript, and models) are stored here.

### 2. GitHub Pages (Website Hosting)

GitHub automatically converts your code into a live website.

👉 Example:  
https://gargsrishti.github.io/ar-menu/

### 3. User Flow

- Website opens  
- Menu appears  
- User clicks item  
- 3D model loads  

---

## ⚙️ Step 1 — Adding AR Support using model-viewer

To enable AR in the browser, we use `<model-viewer>`.

### Add this in `<head>`:

```html
<script type="module" src="https://ajax.googleapis.com/ajax/libs/model-viewer/3.4.0/model-viewer.min.js"></script>
```

### Add this inside `<body>`:

```html
<model-viewer
  src="models/pizza.glb"
  alt="Pizza"
  ar
  ar-modes="webxr scene-viewer quick-look"
  camera-controls
  auto-rotate
  style="width: 100%; height: 300px;">
</model-viewer>
```

👉 This automatically adds the **“View in your space” AR button**

---

## 🍕 Step 2 — Adding 3D Models

Download models from:  
👉 https://poly.pizza

### Folder Structure:

```text
ar-menu/
│── index.html
│── models/
│   ├── pizza.glb
│   ├── burger.glb
│   └── pasta.glb
```

Upload these files to GitHub.

---

## 🔄 Step 3 — Switching Dishes (JavaScript)

```javascript
const dishes = [
  {
    name: "Pizza",
    price: "₹299",
    model: "models/pizza.glb"
  },
  {
    name: "Burger",
    price: "₹199",
    model: "models/burger.glb"
  }
];

let current = 0;

function loadDish(i) {
  document.querySelector('model-viewer').src = dishes[i].model;
}

function nextDish() {
  current = (current + 1) % dishes.length;
  loadDish(current);
}
```

👉 This enables arrow-based navigation between dishes.

---

## 🥗 Step 4 — Ingredients & Nutrition

```html
<div class="info">
  <p>Ingredients: Tomato, Cheese</p>
  <p>Calories: 250 kcal</p>
</div>
```

👉 Keep it simple (basic nutrition information is sufficient).

---

## 📱 Step 5 — QR Code Integration

This is the final and most important step.

### Steps:

- Open: https://qrcode-monkey.com  
  OR https://qr.io  

- Paste your website URL:

```text
https://gargsuhani.github.io/ar-menu/
```

- Generate QR code  
- Download PNG  
- Print and place it on the table  

---

## 🔄 Final Working Flow

Scan QR → Website opens → Menu visible → Click item →  
3D model loads → Click AR → View on table  

---

## 🚀 Conclusion

This project demonstrates how web-based AR can be integrated into real-world applications like restaurant menus.

By combining:

- GitHub hosting  
- model-viewer  
- QR technology  

we created a simple yet powerful AR experience without requiring a mobile application.