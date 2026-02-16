# 🍕 High Level Design of Pizza Visualization System

**Author:** Akarsh  
**Date:** February 13, 2026  

---

## 📌 Project Overview

This project presents a **Hybrid Augmented Reality (AR) system** that combines:

- QR Code-based Data Retrieval
- SLAM-based Surface Detection
- 3D Object Placement on Real-world Tables

Unlike traditional marker-based AR systems, this architecture separates:

- QR Code → Data Trigger  
- SLAM → Real-world Surface Placement  

This enables a more immersive and technically advanced AR experience.

---

## 🎯 System Capabilities

The system allows users to:

1. Scan a QR code on a restaurant menu  
2. Load the complete pizza menu dynamically  
3. Select a specific pizza  
4. View a 3D pizza model rendered on the real table  

---

## 🧠 Architecture Overview

### 🔹 Hybrid Model

| Component | Responsibility |
|-----------|---------------|
| QR Code | Data Retrieval |
| SLAM | Surface Detection |
| User Selection | 3D Rendering |

> ⚠️ The pizza does **NOT** appear on the QR marker.  
> The QR only triggers data loading.

---

## 📷 Marker Detection & Tracking Module (QR-Based)

### 1️⃣ Camera Frame Acquisition

The mobile camera continuously captures frames (30–60 FPS).

Preprocessing steps:

- Grayscale conversion  
- Edge detection  
- Corner detection  

---

### 2️⃣ Feature Point Extraction

AR SDKs used:

- ARCore  
- ARKit  
- Vuforia  
- AR Foundation  

#### Algorithms Used Internally

- ORB (Oriented FAST and Rotated BRIEF)
- FAST Corner Detection
- SIFT / SURF (legacy)

QR codes are ideal due to:

- High black-white contrast  
- Strong geometric structure  

Each detected feature becomes a **2D coordinate in image space**.

---

### 3️⃣ Feature Matching

- Live camera features  
- Stored QR reference features  

Matched using descriptor comparison.

If sufficient matches are found → **Marker detected successfully.**

---

### 4️⃣ Pose Estimation

The system computes:

- Rotation (R)  
- Translation (T)  

Using:

- Perspective-n-Point (PnP)
- Homography Matrix

This determines QR position and orientation in 3D space.

---

## 🧠 Surface Detection Using SLAM

### What is SLAM?

**SLAM = Simultaneous Localization and Mapping**

It performs:

1. Environment mapping  
2. Device movement tracking  

---

### Step 1 — Environmental Feature Tracking

Detected features:

- Table edges  
- Wood patterns  
- Corners  
- Texture variations  

---

### Step 2 — Motion Tracking

Combines:

- Camera input  
- Gyroscope  
- Accelerometer  

---

### Step 3 — Point Cloud Creation

Tracked features form a **sparse 3D point cloud**.

---

### Step 4 — Plane Detection

Using **RANSAC**:

- Coplanar points clustered  
- Surface model fitted  

If enough horizontal points exist → Plane detected.

---

## 🔄 Complete System Flow

### Step 1 — QR Scan

- QR detected  
- JSON menu loaded  
- UI updates  
- No 3D object rendered  

---

### Step 2 — SLAM Activation

- User moves phone  
- Table surface detected  
- Plane visualization appears  

---

### Step 3 — Pizza Selection

- 3D prefab instantiated  
- Hit test performed  
- Object anchored to plane  
- Pizza appears  

---

## 🎯 Hit Testing & Object Placement

When placing pizza:

1. User taps screen (x, y)  
2. Ray cast from camera  
3. Ray intersects detected plane  
4. Intersection coordinate returned  
5. Object placed  

---

### 📐 Ray Equation

P = O + tD  

Where:

- O = Camera origin  
- D = Direction vector  
- t = Scalar  

---

### 📐 Plane Equation

Ax + By + Cz + D = 0  

Solving ray-plane intersection gives world coordinate.

---

## 🏗 Architectural Options

### Option A — Pure Marker-Based

- Pizza appears directly on QR  
- Simpler implementation  
- Lower computational load  

---

### Option B — Hybrid (Recommended)

- QR = Data trigger only  
- SLAM = Real-world placement  

#### Advantages

- More immersive  
- Strong academic value  
- Better UX  

---

## ⚠️ Engineering Note

If pizza is placed relative to table:

- QR does NOT control object position  
- It only triggers data loading  

Placement depends on:

- SLAM  
- Plane detection  
- Hit testing  

---

## 🧩 Technical Components Used

- Computer Vision  
- Feature Detection  
- Pose Estimation  
- SLAM  
- Plane Detection  
- Ray Casting  
- 3D Rendering  

---

## 🚀 Conclusion

This Hybrid AR architecture separates:

**Data Retrieval (QR)**  
from  
**Spatial Placement (SLAM)**  

Creating a scalable and immersive AR system suitable for:

- Restaurant visualization  
- AR commerce  
- Educational AR  
- Advanced HCI research  
