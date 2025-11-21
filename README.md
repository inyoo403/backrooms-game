# The Backrooms: WebGL Experience

A browser-based 3D horror exploration game inspired by "The Backrooms" creepypasta. Built with **Three.js** for rendering and **Cannon-es** for physics simulation. The game features a liminal space atmosphere, puzzle-solving elements, and a hybrid 2D/3D gameplay loop.

## 🛠 Tech Stack

* **Language:** TypeScript
* **Build Tool:** Vite
* **3D Rendering:** Three.js
* **Physics Engine:** Cannon-es
* **Model Loading:** GLTFLoader
* **UI/Styling:** HTML5, CSS3

## 🌟 Key Features

* **Physics-Based Controller:** Smooth first-person movement using a physics sphere with damping and collision detection.
* **Atmospheric Rendering:** Custom fog settings, mono-colored textures, and lighting to recreate the unsettling "liminal space" vibe.
* **Interaction System:** Distance-based trigger system that allows players to interact with objects using the 'E' key.
* **Hybrid Gameplay:** Seamless integration of 2D HTML/CSS overlays (Simon Says minigame) within the 3D WebGL context.
* **Inventory System:** visual inventory bar tracking collected items (Red, Blue, Green balls).
* **Dynamic Environment:**
    * Flashlight mechanics attached to the camera.
    * Flickering fluorescent lights.
    * Conditional object rendering (Escape trigger appears only after collecting all items).

## 🎮 Controls

| Key | Action |
| :--- | :--- |
| **W, A, S, D** | Move Character |
| **Shift** | Sprint |
| **Mouse** | Look Around |
| **E** | Interact / Start Minigame |
| **Click** | Lock Pointer / Resume Game |

## 🚀 Installation & Setup

1.  **Clone the repository**

    ```bash
    git clone https://github.com/inyoo403/backrooms-game.git
    cd backrooms-game
    ```

2.  **Install dependencies**

    ```bash
    npm install
    ```

3.  **Run development server**

    ```bash
    npm run dev
    ```

4.  **Build for production**

    ```bash
    npm run build
    ```

## 📂 Project Structure

```
src/
├── main.ts          # Main entry point, game loop, scene setup
├── Player.ts        # Physics-based player controller logic
├── Inventory.ts     # Inventory UI and state management
├── SimonGame.ts     # 2D Minigame logic and DOM manipulation
├── style.css        # Global styles and UI overlays
└── ...
```

---

*Developed by Inho Yoo*

