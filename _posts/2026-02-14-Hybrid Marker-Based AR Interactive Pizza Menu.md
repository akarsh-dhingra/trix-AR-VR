---
layout: post
title: "Hybrid Marker-Based AR Interactive Pizza Menu
"
date: 2026-02-14
categories: [Akarsh]
---


# 🍕 Hybrid Augmented Reality (AR) Pizza Visualization System

## 📌 Project Overview

This project presents a **Hybrid Augmented Reality (AR) system** that combines:

- **QR Code-based Data Retrieval**
- **SLAM-based Surface Detection**
- **3D Object Placement on Real-world Tables**

Unlike traditional marker-based AR systems, this architecture separates:

- **QR Code → Data Trigger**
- **SLAM → Real-world Surface Placement**

This enables a more immersive and technically advanced AR experience.

---

# 🎯 System Capabilities

The system allows users to:

1. Scan a QR code on a restaurant menu.
2. Load the complete pizza menu dynamically.
3. Select a specific pizza.
4. View a 3D pizza model rendered on the real table in front of them.

---

# 🧠 Architecture Overview

## 🔹 Hybrid Model

| Component | Responsibility |
|-----------|---------------|
| QR Code | Data Retrieval |
| SLAM | Surface Detection |
| User Selection | 3D Rendering |

> ⚠️ The pizza does **NOT** appear on the QR marker.  
> The QR only triggers data loading.

---

# 📷 Marker Detection & Tracking Module (QR-Based)

## 1️⃣ Camera Frame Acquisition

The mobile camera continuously captures frames (30–60 FPS).

Each frame undergoes preprocessing:

- Grayscale conversion  
- Edge detection  
- Corner detection  

These steps prepare the frame for feature extraction.

---

## 2️⃣ Feature Point Extraction

AR SDKs such as:

- ARCore  
- ARKit  
- Vuforia  
- AR Foundation  

detect distinct visual features from the QR image.

### Algorithms Used Internally

- ORB (Oriented FAST and Rotated BRIEF)
- FAST Corner Detection
- SIFT / SURF (legacy methods)

These algorithms:

- Detect corners  
- Identify edges  
- Extract unique pixel patterns  

QR codes are ideal due to:

- High black-white contrast  
- Strong geometric structure  

Each detected feature becomes a **2D coordinate in image space**.

---

## 3️⃣ Feature Matching

The system stores a reference image of the QR marker.

During runtime:

- Live camera features  
  are matched with  
- Stored QR reference features  

Using descriptor matching.

If sufficient matches are found → **Marker detected successfully.**

---

## 4️⃣ Pose Estimation

Once detected, the system computes:

- **Rotation (R)**
- **Translation (T)**

Using:

- Perspective-n-Point (PnP)
- Homography Matrix

This determines:

- Position of QR in 3D space
- Orientation relative to camera

A transformation matrix is generated, creating a virtual coordinate system.

---

# 🧠 Surface Detection Using SLAM

## What is SLAM?

**SLAM = Simultaneous Localization and Mapping**

It performs two tasks simultaneously:

1. Maps the environment.
2. Tracks device movement in 3D space.

---

## Step 1️⃣ Environmental Feature Tracking

The camera detects natural feature points such as:

- Table edges
- Wood patterns
- Corners
- Texture variations

These are environmental features — different from QR features.

---

## Step 2️⃣ Motion Tracking

The system combines:

- Camera input
- Gyroscope
- Accelerometer

To determine device movement in 3D space.

---

## Step 3️⃣ Point Cloud Creation

Tracked feature points are converted into a **sparse 3D map**.

This forms a point cloud representation of the environment.

---

## Step 4️⃣ Plane Detection

Using algorithms like **RANSAC**:

- Coplanar points are clustered.
- A flat surface model is fitted.

If sufficient horizontal points exist → A plane is detected.

Examples:
- Table surface
- Floor

---

# 🔄 Complete System Flow

## 🔹 Step 1 — QR Scan

- Camera detects QR code.
- QR is decoded.
- JSON menu data is retrieved.
- Pizza list loads in UI.
- No 3D object rendered yet.

---

## 🔹 Step 2 — SLAM Activation

- User moves phone.
- System detects table surface.
- Plane visualization appears.

---

## 🔹 Step 3 — Pizza Selection

When user selects a pizza:

- Corresponding 3D prefab is instantiated.
- System performs a hit test.
- Object is anchored to detected plane.
- Pizza appears on the table.

---

# 🎯 Hit Testing & Object Placement (Mathematical Insight)

When placing the pizza:

1. User taps screen at coordinates (x, y).
2. System casts a ray from camera into 3D world.
3. Ray intersects detected plane.
4. Intersection point is returned.
5. 3D object placed at that coordinate.

---

## 📐 Ray Equation

P = O + tD

Where:

- O = Camera origin  
- D = Direction vector  
- t = Scalar  

---

## 📐 Plane Equation

Ax + By + Cz + D = 0


Solving the ray-plane intersection provides the precise world coordinate.

---

# 🏗 Architectural Options

## Option A — Pure Marker-Based

- Pizza appears directly on QR.
- Simpler implementation.
- Lower computational load.

---

## Option B — Hybrid (Recommended)

- QR = Data trigger only.
- SLAM = Real-world placement.
- Pizza appears on table.

### Advantages

- More immersive
- Technically advanced
- Stronger academic value
- Better user experience

---

# ⚠️ Important Engineering Note

If the pizza is placed relative to the table:

- The QR marker does NOT control object position.
- It only:
  - Triggers data loading
  - Starts AR session

Object placement depends entirely on:

- SLAM
- Plane detection
- Hit testing

---

# 🧩 Technical Components Used

- Computer Vision
- Feature Detection Algorithms
- Pose Estimation
- SLAM
- Plane Detection
- Ray Casting
- 3D Rendering Engine

---

# 🚀 Conclusion

This Hybrid AR architecture separates:

**Data Retrieval (QR)**  
from  
**Spatial Placement (SLAM)**  

This creates a scalable, immersive, and academically robust AR system suitable for:

- Restaurant visualization systems
- Interactive AR commerce
- Educational AR applications
- Advanced HCI research projects

---

