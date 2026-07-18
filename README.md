# AI Gesture-Controlled Virtual Mouse

A computer vision application that leverages a webcam to control system mouse movements and mouse actions (clicks, drags, scrolls) through hand gestures.

> [!WARNING]  
> **Legacy Architecture Warning:** This project uses the legacy MediaPipe Solutions API (`mp.solutions.hands`) and requires specific older versions of Python and dependencies to run properly. 

---

## 🛠 Prerequisites & Requirements

Because the legacy MediaPipe module is incompatible with newer package versions (such as NumPy 2.0+) and newer Python releases, your environment **must** match the constraints below:

* **Python Version:** `3.8`, `3.9`, `3.10`, or `3.11` (**64-bit only**). Python 3.12+ is not supported.
* **Operating System:** Windows, macOS, or Linux.
* **Hardware:** A functional webcam.

---

## 🚀 Setup & Installation

We recommend running this project inside an isolated virtual environment (`venv`) to prevent version conflicts with your global Python installation.

### 1. Create a Python 3.11 Virtual Environment
Open your terminal in the project directory and run the command for your OS:

* **Windows:**
  ```bash
  py -3.11 -m venv .venv
  ```
* **Mac / Linux:**
  ```bash
  python3.11 -m venv .venv
  ```

### 2. Activate the Environment
* **Windows (PowerShell):**
  ```bash
  .venv\Scripts\Activate.ps1
  ```
* **Mac / Linux:**
  ```bash
  source .venv/bin/activate
  ```

### 3. Install the Legacy Dependencies
Create a `requirements.txt` file in your directory using the specifications provided below, then run:
```bash
pip install -r requirements.txt
```

#### `requirements.txt` contents:
```text
mediapipe==0.10.21
numpy<2.0.0
opencv-python
pyautogui
```

---

## 🎮 How to Use & Gestures

Run the python script from your terminal:
```bash
python your_script_name.py
```

Keep your hand within the magenta Region of Interest (ROI) box drawn on the screen. The script tracks the following finger combinations to perform actions:

| Finger Setup | Gesture Actions |
| :--- | :--- |
| **Index Up** | Moves the cursor smoothly across the screen. |
| **Index + Middle Up** | Performs a standard **Left Click**. If held up for over 50 frames, triggers a **Double Click**. |
| **Index + Middle + Ring Up** | Triggers a **Right Click**. |
| **Index + Middle + Ring + Pinky Up** | **Vertical Scrolling**. The scroll direction is mapped dynamically to the movement of your middle finger relative to its initial reference position. |
| **All 5 Fingers Up** | Triggers a **Mouse Drag** (left mouse button held down). Allows you to drag objects around until you lower your fingers. |

* **Exit Program:** Press the **`q`** key while focused on the webcam window to safely destroy all windows and stop execution.

---

## ⚠️ Troubleshooting

* **"No matching distribution found for mediapipe":** This means you are accidentally trying to install inside a Python 3.12 or 3.13 environment. Double-check your active version using `python --version`.
* **PyAutoGUI Failsafes:** PyAutoGUI has built-in failsafes. While `FAILSAFE=False` is set in this code, if your cursor gets stuck or acts erratically, moving your physical mouse to any of the four extreme corners of your screen will manually interrupt the automated inputs.
