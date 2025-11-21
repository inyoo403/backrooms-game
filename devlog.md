# Development Log: The Backrooms WebGL Project

**Author:** Inho Yoo

**Date:** November 2023

**Topic:** Building an immersive 3D web game with physics and hybrid UI.

---

## 1. Project Overview

The goal of this project was to recreate the eerie atmosphere of "The Backrooms" in a web browser while implementing solid gameplay mechanics including physics-based movement, puzzle interactions, and inventory management.

## 2. Key Implementations & Technical Decisions

### 2.1 Physics-Based Player Controller

Instead of simple coordinate translations, I integrated **Cannon-es** to handle movement logic.

* **Implementation:** Created a `Player` class that synchronizes a Three.js `Camera` with a Cannon-es `Sphere` body.

* **Why:** A physics body prevents players from walking through walls and allows for natural interactions with the environment.

* **Code Highlight:**

    ```typescript
    // Synchronization in the update loop
    this.camera.position.set(
        this.body.position.x,
        this.body.position.y + this.height,
        this.body.position.z
    );
    ```

* **Control Logic:** Implemented `PointerLockControls` for standard FPS aiming. Added a `setControls(boolean)` method to toggle between 3D movement and 2D cursor mode for minigames.

### 2.2 Creating the "Liminal" Atmosphere

The visual style defines this game. I focused on lighting and material uniformity.

* **Materials:** Instead of using complex textures, I used `MeshStandardMaterial` with specific hex colors (e.g., `#d1c485` for walls) and adjusted `roughness` to distinguish between carpet and wallpaper.

* **Smart Coloring:** Implemented a logic in the GLTFLoader to automatically detect floor vs. walls using normal vectors (`normal.y > 0.5`) and apply different materials accordingly.

* **Fog & Lighting:** Used `THREE.Fog` with a color matching the background to hide the map boundaries, creating a sense of infinity. Added a `SpotLight` to the camera (flashlight) to solve visibility issues in the dark ambient lighting (`0.4` intensity).

### 2.3 Trigger System & Interaction

I needed a way for the player to interact with specific zones (rooms).

* **Distance Check:** Instead of expensive Raycasting every frame for triggers, I used a simple Euclidean distance check (`distanceTo`) between the player and predefined trigger coordinates.

* **Visual Cues:** Added rotating wireframe boxes to indicate interactive areas.

* **UI Prompt:** A dynamic HTML overlay ("[E] Start Minigame") appears when the player enters a trigger zone.

### 2.4 Hybrid 2D/3D Architecture (The Minigame)

A unique challenge was integrating a 2D DOM-based puzzle into a 3D WebGL context.

* **State Management:** Created a global `isGameActive` flag. When active, the 3D physics loop continues (time flows), but the Player Controller stops processing inputs (`player.setControls(false)`).

* **Simon Game Logic:** Implemented a `SimonGame` class that dynamically creates DOM elements. It handles the sequence generation, user input validation, and callbacks for winning/losing.

* **Seamless Transition:** Upon winning, the inventory updates immediately, and the pointer lock is re-engaged without breaking immersion.

### 2.5 Game Loop & Win Condition

The `main.ts` acts as the central conductor.

* **Inventory:** Checking for collected items ('red', 'blue', 'green').

* **Dynamic World Changes:** Once all items are collected, the `checkWinCondition()` function activates the previously hidden "Escape Trigger" (Blue Box) at the center of the map.

## 3. Challenges & Solutions

* **Issue:** The player camera clipped through walls when standing too close.

    * **Fix:** Adjusted the `PerspectiveCamera`'s near plane from `0.1` to `0.2` and ensured the physics body radius kept the camera at a safe distance.

* **Issue:** The map felt too flat and confusing.

    * **Fix:** Added a Flashlight and decreased ambient light to create contrast/depth. Differentiated floor and wall colors slightly.

## 4. Conclusion

This project successfully demonstrates how to combine low-level graphics libraries (Three.js) with physics engines and standard DOM manipulation to create a cohesive game experience.

---

*Devlog created by Inho Yoo*

