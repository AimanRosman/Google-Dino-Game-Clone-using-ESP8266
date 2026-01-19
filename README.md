# Google Dino Game Clone for ESP8266/ESP32

![License](https://img.shields.io/github/license/AimanRosman/Google-Dino-Game-Clone-using-ESP8266?style=for-the-badge)
![Stars](https://img.shields.io/github/stars/AimanRosman/Google-Dino-Game-Clone-using-ESP8266?style=for-the-badge)
![Forks](https://img.shields.io/github/forks/AimanRosman/Google-Dino-Game-Clone-using-ESP8266?style=for-the-badge)
![Issues](https://img.shields.io/github/issues/AimanRosman/Google-Dino-Game-Clone-using-ESP8266?style=for-the-badge)

A faithful recreation of the classic Google Chrome Dinosaur Game running on ESP8266/ESP32 microcontrollers with an OLED display.

![Game Start](https://github.com/user-attachments/assets/ac7916f3-05b2-4f62-af7a-a48e0e611b45)

## 📖 Table of Contents
- [Features](#-features)
- [Hardware Required](#-hardware-required)
- [Wiring Diagram](#-wiring-diagram)
- [Installation](#-installation)
- [How to Play](#-how-to-play)
- [Customization](#-customization)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features
- **Classic Gameplay**: Jump over cacti and survive as long as you can.
- **OLED Graphics**: Smooth rendering on 128x64 OLED displays.
- **Sound Effects**: Buzzer feedback for jumps and game over melodies.
- **Score Tracking**: Real-time score display.
- **Increasing Difficulty**: Obstacles move faster as you progress.

## 🛠 Hardware Required
To build this project, you will need:
- **Microcontroller**: ESP8266 (NodeMCU/WeMos D1 Mini) or ESP32
- **Display**: 0.96" OLED Display (128x64, I2C)
- **Input**: Push Button (Tactile Switch)
- **Audio**: Passive Buzzer
- **Breadboard & Jumper Wires**

## 🔌 Wiring Diagram

| Component | ESP8266 Pin | ESP32 Pin (Typical) |
|-----------|-------------|---------------------|
| **OLED SDA** | D2 (GPIO 4) | GPIO 21 |
| **OLED SCL** | D1 (GPIO 5) | GPIO 22 |
| **Button** | D3 (GPIO 0) | GPIO 4 |
| **Buzzer** | D5 (GPIO 14) | GPIO 5 |

> **Note**: Pin definitions can be modified in the code (`game.ino`) to match your specific setup.

## 🚀 Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/AimanRosman/Google-Dino-Game-Clone-using-ESP8266.git
   ```

2. **Open in Arduino IDE**
   - Navigate to the `game` folder.
   - Open `game.ino`.

3. **Install Dependencies**
   - Go to `Sketch` -> `Include Library` -> `Manage Libraries...`
   - Search for and install:
     - **Adafruit SSD1306**
     - **Adafruit GFX Library**

4. **Upload**
   - Select your board (e.g., NodeMCU 1.0 or ESP32 Dev Module).
   - Select the correct COM port.
   - Click **Upload**.

## 🎮 How to Play
1. Power on the device.
2. The game will start automatically.
3. Press the **Push Button** to jump over incoming obstacles.
4. Avoid hitting the cacti!
5. If you crash, the game ends with a "GAME OVER" screen and a melody.
6. Press the button again to restart.

## ⚙ Customization
You can tweak the game dynamics in `game.ino`:

```cpp
int jumpHeight = 15;      // Adjust jump height
int maxJumpFrames = 15;   // Adjust jump duration
int obstacleX -= 4;       // Adjust initial speed (higher = faster)
```

## 🤝 Contributing
Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests.

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
*Check out the project in action on [TikTok](https://vt.tiktok.com/ZSjaQG491/)*
