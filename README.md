# NeoPIxel-Lantern
A colorful NeoPixel LED project using MicroPython
# 🌟 Interactive NeoPixel Lantern with Chinese Knot
**By Coco**  

## 📌 Introduction  
This project is an interactive LED lantern inspired by traditional Chinese lanterns with a modern RGB lighting system. The lantern integrates a **Chinese knot with copper tape** on both sides, allowing the user to change colors dynamically when lifted and hold the color when placed down.  

The lantern uses a **NeoPixel LED strip** controlled by an **ESP32 microcontroller** running **MicroPython**. The lighting effects include **color transitions, breathing effects, a dynamic rainbow mode, and wave animations**, creating a vibrant and immersive experience.  

## 📌 State Diagram  
Below is the state diagram representing the interactive behavior of the lantern:  

<img width="635" alt="截屏2025-02-27 下午11 16 41" src="https://github.com/user-attachments/assets/31489e0e-83a9-4b0a-989d-0391144c46fe" /> 

## 📌 Hardware  
The following hardware components were used in this project:  
- **ESP32 (M5Stack AtomS3 Lite)** – Microcontroller for controlling the NeoPixel LED strip  
- **NeoPixel LED strip (30 LEDs)** – RGB lighting output  
- **Copper tape** – Used as a capacitive sensor to detect interaction  
- **Chinese knot decoration** – Integrated as part of the interactive element  
- **Paper or translucent acrylic** – Lantern casing for diffusing light  

### 📷 Hardware Wiring Diagram  
*(Include an image here showing your wiring setup, or a Fritzing diagram.)*  

## 📌 Firmware (MicroPython Code)  
The firmware detects the **copper tape input** and controls the LED strip accordingly.  

### **Features**  
✅ Detects the copper tape input (HIGH = lifted, LOW = placed down)  
✅ Cycles through predefined colors **(Red, Yellow, Green, Purple, Blue)**  
✅ Plays a **dynamic rainbow effect**   
✅ Includes **breathing and wave effects** for smooth transitions  
✅ **Instantly stops animation and changes colors when lifted**  

https://github.com/user-attachments/assets/283eecd3-9bdd-4955-8e44-0da056249868

### **Code Snippet**
```python
from machine import Pin
from neopixel import NeoPixel
import time

# Initialize button (Copper Tape)
button = Pin(1, Pin.IN, Pin.PULL_UP)  
button_last_state = 1  

# Initialize NeoPixel LED Strip
num_pixels = 30
np = NeoPixel(Pin(7), num_pixels)

# Color List
COLORS = [(255, 0, 0), (255, 255, 0), (0, 255, 0), (128, 0, 128), (0, 0, 255), "rainbow"]
color_index = 0  

# Detect button press and switch colors
while True:
    if button.value() == 0 and button_last_state == 1:
        color_index = (color_index + 1) % len(COLORS)
        print("Switching to:", COLORS[color_index])  
        while button.value() == 0:
            time.sleep_ms(10)
        np.fill(COLORS[color_index] if COLORS[color_index] != "rainbow" else (255, 255, 255))
        np.write()
    button_last_state = button.value()






