# Slot Machine - WebGL Project

A modular, DOTween-powered slot machine reel system built in Unity. This project demonstrates synchronized reel behavior, randomized logic, and responsive UI animations.

## Game Overview
This is a classic 3-reel slot machine game. The logic is handled through a decoupled system where the `SpinManager` dictates the results, and individual `ReelMoveManager` components handle the visual "spin and snap" behavior.

* **Reels:** 3 independent reels with wrapping coordinate logic.
* **Scoring:** * **3-of-a-kind:** Jackpot Win.
    * **2-of-a-kind:** "Nice Try" consolation.
    * **No match:** Loss.
* **UI:** Animated results pop-up with scaling/fading effects.

## Instructions to Run WebGL Build
1.  **Open Index:** Locate the `index.html` file in the `Build/` folder.
2.  **Local Server (Important):** Most modern browsers block WebGL files run directly from the file system (`file://`). Use a local server (like VS Code's **Live Server** extension or Python's `http.server`) to run the folder.
3.  **Controls:** Simply click the **Spin Button** to initiate the sequence.

## Bonus Features
* **Staggered Starts:** Reels don't stop all at once; they are offset by 0.15s to build anticipation (standard industry feel).
* **Elastic Landing:** Used `Ease.OutBack` on the final snap to give the symbols a weighted "bounce" when they hit the stop line.
* **Coordinate Normalization:** The system automatically resets Y-positions after every spin to prevent floating-point errors during long sessions.

## My Approach
When building the reel logic, I avoided using a massive vertical strip of actual GameObjects. Instead:

* **Coordinate Wrapping:** I implemented a "teleport" logic. When a symbol goes past the `topPosition`, it jumps back to the `bottomPosition`. This allows for an "infinite" spin using only a small set of UI elements.
* **Pre-determined Results:** To ensure the game feels fair, the symbols are picked *before* the reels start moving. This allows the reels to calculate exactly how far they need to travel during the deceleration phase to land perfectly on the target index.
* **State Management:** Used a simple `isSpinning` flag to prevent "spam clicking" which could break the animation coroutines.
* **UI Polish:** Leveraged `CanvasGroup` for the results pop-up to allow for smooth alpha fading, which looks much cleaner than simply toggling the object on and off.

---

### Tech Stack
* **Engine:** Unity 2022.3+
* **Language:** C#
* **Plugins:** DOTween (Used for all smooth UI transitions and reel snapping).
