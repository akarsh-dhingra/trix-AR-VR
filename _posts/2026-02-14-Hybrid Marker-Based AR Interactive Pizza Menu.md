---
layout: post
title: "Hybrid Marker-Based AR Interactive Pizza Menu
"
date: 2026-02-14
categories: [Akarsh]
---


The project is a Hybrid Augmented Reality (AR) system, with it's input module as follows that combines:

QR Code-based Data Retrieval

SLAM-based Surface Detection

3D Object Placement on Real-world Tables

The system allows users to:

Scan a QR code on a restaurant menu.

Load the complete pizza menu dynamically.

Select a specific pizza.

View a 3D pizza model rendered on the table in front of them.

Unlike traditional marker-based AR where the object appears on the marker itself, this system uses:

QR code → Data trigger

SLAM → Real-world surface placement

🧠 Marker Detection & Tracking Module (QR-Based)
1️⃣ Camera Frame Acquisition

The mobile camera continuously captures frames (30–60 FPS).

Each frame undergoes:

Grayscale conversion

Edge detection

Corner detection

These preprocessing steps prepare the image for feature extraction.

2️⃣ Feature Point Extraction

AR SDKs (ARCore, ARKit, Vuforia, AR Foundation) detect distinct visual features from the QR image.

Common algorithms used internally:

ORB (Oriented FAST and Rotated BRIEF)

FAST Corner Detection

SIFT / SURF (older methods)

These algorithms:

Detect corners

Identify edges

Extract unique pixel patterns

Since QR codes have strong black-white contrast and geometric corners, they are ideal for fast detection.

Each detected feature becomes a 2D coordinate in image space.

3️⃣ Feature Matching

The AR system stores a reference image of the QR marker.

During runtime:

Live camera frame features
are compared with

Stored QR reference features

Using descriptor matching:

Corresponding feature points are matched.

If enough matches are found → Marker detected successfully.

4️⃣ Pose Estimation

Once the QR is detected, the system calculates:

Rotation (R)

Translation (T)

Using:

Perspective-n-Point (PnP) algorithm

Homography matrix

This determines:

Position of the QR in 3D space

Orientation relative to the camera

A transformation matrix is computed, creating a virtual coordinate system anchored to the QR.

This enables accurate 3D rendering.

🧠 Hybrid Architecture: QR for Data + SLAM for Placement
Concept

QR Code → Data Retrieval
SLAM → Surface Detection
User Selection → 3D Rendering on Table

The pizza does NOT appear on the QR marker.

Instead:

QR triggers menu loading.

SLAM detects the real-world table.

The selected pizza is rendered on the table.

🧠 Surface Detection Using SLAM

SLAM = Simultaneous Localization and Mapping

It performs two tasks simultaneously:

Maps the surrounding environment.

Tracks the phone's movement in space.

Step 1️⃣ Feature Tracking in Environment

The camera detects natural feature points such as:

Table edges

Wood patterns

Corners

Texture variations

These are different from QR feature points — they are environmental.

Step 2️⃣ Motion Tracking

The system combines:

Camera data

Gyroscope

Accelerometer

To determine how the phone moves in 3D space.

Step 3️⃣ Point Cloud Creation

Tracked feature points are converted into a sparse 3D map.

This creates a point cloud representation of the environment.

Step 4️⃣ Plane Detection

Using algorithms like RANSAC:

The system clusters coplanar points.

Fits a flat surface model.

If enough horizontal points exist → A plane is detected.

Examples:

Table surface

Floor

🧠 System Flow (Step-by-Step)
🔹 Step 1 — QR Scan

Camera detects QR code.

QR is decoded.

JSON menu data is retrieved.

Pizza list is loaded into UI.

(No 3D object rendered yet.)

🔹 Step 2 — SLAM Activation

User moves phone around.

System detects table surface.

Plane visualization appears.

🔹 Step 3 — Pizza Selection

When user selects a pizza:

Corresponding 3D prefab is instantiated.

System performs a hit test.

Object is anchored to detected plane.

Pizza appears on table.

🧠 Hit Testing & Object Placement (Mathematical Insight)

When placing the pizza:

User taps screen at coordinates (x, y)

System casts a ray from camera into 3D world

Ray intersects detected plane

Intersection point is returned

3D object placed at that coordinate

Ray equation:

P = O + tD

Where:

O = camera origin

D = direction vector

t = scalar

Plane equation:

Ax + By + Cz + D = 0

Solving intersection gives precise world position for placement.

🧠 Architectural Options
Option A — Pure Marker-Based

Pizza appears directly on QR.

Simpler implementation.

Lower computational load.

Option B — Hybrid (Recommended)

QR = Data trigger only.

SLAM = Real-world placement.

Pizza appears on table.

Advantages:

More immersive

More technically advanced

Stronger academic value

Better user experience

⚠️ Important Engineering Note

If the pizza is placed relative to the table:

The QR marker does NOT control the object’s position.

It only:

Triggers data loading

Starts AR session

Object placement depends entirely on SLAM and plane detection.

🚀 Technical Components Used

Computer Vision

Feature Detection Algorithms

Pose Estimation

SLAM (Simultaneous Localization and Mapping)

Plane Detection

Raycasting & Hit Testing

3D Rendering

Mobile Sensor Fusion
