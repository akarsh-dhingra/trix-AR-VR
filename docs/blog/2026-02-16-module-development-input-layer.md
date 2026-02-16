# Module Development: Designing the Input Layer of the AR System

**Author:** Suhani Garg  
**Focus:** AR Architecture · SLAM · Unity · System Design  

---
<p align="center">
  <img src="../../images/arvr1.jpeg" width="500">
</p>

## Why the Input Layer Matters

Before rendering 3D pizzas or designing UI interactions, the AR system must first understand the physical world.

The **Input Layer** is responsible for capturing and interpreting environmental data. Without it, the application cannot:

- Detect surfaces  
- Place 3D objects accurately  
- Maintain spatial stability  
- Respond to user gestures  

This layer forms the foundation of the entire AR experience.

---

## Core Responsibilities of the Input Module

We structured the input module into three functional components:

1. Surface Detection & Plane Tracking  
2. Marker / QR-Based Initialization  
3. User Interaction Handling  

Each component enables real-time AR behavior in a controlled and modular way.

---

## 1. Surface Detection & Plane Tracking

To allow a virtual pizza to appear naturally on a table or floor, the system must detect horizontal planes.

This is achieved using **SLAM (Simultaneous Localization and Mapping)** algorithms.

### What SLAM Enables

SLAM allows the system to:

- Track camera movement in 3D space  
- Map environmental feature points  
- Identify flat surfaces  
- Maintain spatial consistency  

Although AR Foundation abstracts this internally, the underlying processing is handled by:

- **ARCore** (Android)  
- **ARKit** (iOS)  

### Engineering Decision

To optimize performance, we configured:

- Horizontal plane detection only  
- Persistent anchors for object stability  

This reduces computational overhead and improves mobile responsiveness.

---

## 2. Marker / QR-Based Initialization

Our system follows a **hybrid AR approach**.

Instead of placing objects randomly on detected planes, we use:

- A single marker (menu card / QR image)  
- Trigger-based AR scene activation  

### Why a Single Marker?

Using one marker:

- Simplifies system structure  
- Reduces user confusion  
- Ensures consistent experience  
- Improves scalability  

<p align="center">
  <img src="../../images/arvr2.jpeg" width="500">
</p>

Once the marker is scanned:

1. The AR session initializes  
2. The 3D pizza model is instantiated  
3. Navigation UI becomes active  

The marker acts only as an entry trigger — it does not repeatedly reload the scene.

---

## 3. User Interaction Handling

After object placement, the user must interact with it.

The Input Layer therefore manages:

- Touch detection  
- Drag gestures  
- Rotation gestures  
- UI button interactions  

We separated interaction logic from rendering logic to maintain modularity.

### Interaction Flow

1. Detect touch input  
2. Perform raycast from camera  
3. Validate plane hit  
4. Update object transform  

This pipeline ensures a clean separation between sensing and action execution.

---

## Performance Considerations

Since the application runs on mobile devices, optimization was essential.

We improved efficiency by:

- Restricting plane detection types  
- Using optimized 3D assets  
- Limiting redundant sensor polling  
- Avoiding unnecessary scene reloads  

Input processing must remain lightweight to maintain stable frame rates.

---

## Architectural Perspective

From a system design standpoint, the Input Layer acts as:

> The bridge between the physical world and the digital AR environment.

It converts environmental signals into structured spatial data, enabling higher-level modules such as:

- Rendering Engine  
- UI Layer  
- Business Logic Layer  

Without a defined input architecture, AR systems become unstable and unpredictable.

---

## Key Insight

Thinking in modules transforms an idea into an engineered system.

Instead of stating:

> “The app detects surfaces.”

We now define:

- Which algorithm performs detection  
- Which platform module executes it  
- What constraints apply  
- How performance is managed  

This shift from feature description to system architecture marks the transition from conceptual thinking to structured engineering design.
