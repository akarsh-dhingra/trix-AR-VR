---
layout: page
title: AR-VR Project Blog Collection
---

Welcome to our group documentation site.

## Authors

- [Suhani](Blogs/Suhani/)
- [Akarsh](Blogs/Akarsh/)
- [Srishti](Blogs/Srishti/)

# Interactive Marker-Based AR Menu Browsing System

## Project Overview
This project is a marker-based augmented reality (AR) application designed to enhance the traditional food menu experience. By scanning a printed menu containing a QR code or image marker, users can view interactive 3D representations of pizza items directly on the menu. The system allows users to browse multiple pizza variations, explore ingredient details, and view nutritional information, helping them make more informed food choices.

The project focuses on improving decision-making at the point of ordering rather than replacing the menu or implementing online ordering.

---

## Type of Augmented Reality
## **Marker-based AR**
- A predefined menu image/QR code is used as the marker.
- AR content appears only when the marker is detected.

---

## Features

### 1. Menu Scanning
- User scans the menu marker using the AR application.
- A 3D pizza model appears anchored to the menu.

### 2. Arrow-Based Menu Navigation
- Left and right arrows allow browsing through multiple pizza variations.
- Only one scan is required to view all items.
- Prevents the need to rescan the menu for each item.

### 3. Ingredient Interaction
- Individual pizza toppings are clickable.
- On clicking a topping, ingredient details are displayed.
- Helps users understand food composition and allergens.

### 4. Nutrition Information Toggle
- A toggle button displays nutritional information such as calories and dietary type.
- Information can be shown or hidden based on user preference.

---

## Input – Processing – Output

### Input
- Camera feed
- Printed menu image (marker)
- User interactions (arrow taps, ingredient taps, toggle button)

### Processing
- Marker detection
- Selection of pizza models from predefined data
- UI and interaction handling

### Output
- 3D pizza visualization in AR
- Interactive browsing between pizza items
- Ingredient and nutrition information overlays

---

## Technologies Used
- Unity
- AR Foundation
- C#
- Android platform

---

## How to Run the Project
1. Install the AR application APK on an Android device.
2. Open the application.
3. Allow camera permissions.
4. Point the camera at the printed menu marker.
5. Use arrows to browse pizza items and interact with features.

---

## Scope and Limitations

### Included
- 5–8 predefined pizza items
- Static 3D models
- Local data storage
- Simple UI-based interaction

### Not Included
- Online ordering or payment
- AI-based recommendations
- Real-time customization
- Dynamic size fitting or physics

---

## Conclusion
This project demonstrates how marker-based AR can be extended beyond simple visualization by incorporating interaction, navigation, and contextual information. The system provides a practical and user-friendly example of AR usage suitable for beginner-level implementation while addressing a real-world problem.

---

