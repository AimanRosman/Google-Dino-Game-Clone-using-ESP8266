# ESP8266 OLED Dinosaur Game

A small Arduino game inspired by Chrome's offline dinosaur runner. An ESP8266 drives a `128 x 64` SSD1306 OLED, reads a push button for jumping, and plays buzzer feedback. The project demonstrates a frame-based game loop, simple graphics, collision checks, input handling, and sound generation on constrained hardware.

![Original hardware demonstration](https://github.com/user-attachments/assets/ac7916f3-05b2-4f62-af7a-a48e0e611b45)

## Implemented behavior

- A drawn dinosaur and a single obstacle moving across the OLED.
- Button-triggered jumping with configurable height and duration.
- Ground-level collision detection and a restart flow.
- On-screen scoring from elapsed time, obstacle passes, and jump overlap.
- Short buzzer feedback during successful overlap and a game-over melody from `song.h`.

Obstacle speed is fixed in the committed code; increasing difficulty is not implemented. The graphics and scoring are a simplified interpretation of the original game.

## Hardware and dependencies

- ESP8266 board with the Arduino `D5`/`D6` pin aliases, such as NodeMCU or a compatible D1 mini board.
- I2C SSD1306 OLED, `128 x 64`, configured at address `0x3C`.
- Momentary button, suitable buzzer, breadboard/wiring, and USB power.
- Arduino IDE with ESP8266 board support.
- `Adafruit SSD1306` and `Adafruit GFX Library`, including their required dependencies. `Wire` comes with the board package.

The project does not pin board-package or library versions. Record those versions with any tested hardware build.

### Wiring

| Component signal | ESP8266 setting |
| --- | --- |
| OLED SDA | Default `Wire` SDA; typically D2 / GPIO `4` on NodeMCU |
| OLED SCL | Default `Wire` SCL; typically D1 / GPIO `5` on NodeMCU |
| Button input | **D6 / GPIO `12`**, as declared by `BUTTON_PIN` |
| Button other terminal | Ground; firmware uses `INPUT_PULLUP` |
| Buzzer signal | D5 / GPIO `14` |
| Grounds | Common ground |

Use the board and display's supported supply voltages. The sketch does not override the I2C pins, so verify your board's `Wire` defaults.

ESP32 use requires replacing the ESP8266 pin aliases, choosing the appropriate I2C pins, and verifying board/core behavior.

## Build and play

1. Install ESP8266 board support and the Adafruit libraries in Arduino IDE.
2. Open [game/game.ino](game/game.ino). Keep [game/song.h](game/song.h) in the same sketch folder.
3. Connect the hardware using the assignments above and select the correct board and serial port.
4. Compile and upload. If display allocation fails, check the serial monitor at `115200` baud and verify the display address, wiring, and power.
5. The game starts after initialization. Press the button to jump, then press it after a collision to interrupt the melody or restart.

The source uses a 50 ms delay at the end of each loop. Rendering and audio add to that time, so it is not a fixed-rate simulation.

## Customization

| Value in `game.ino` | Default | Effect |
| --- | --- | --- |
| `jumpHeight` | `15` | Jump offset in pixels |
| `maxJumpFrames` | `15` | Jump phase duration |
| `hoverFrames` | `10` | Additional peak frames |
| `obstacleWidth` / `obstacleHeight` | `8` / `10` | Obstacle dimensions |
| `obstacleX -= 4` | `4` pixels per loop | Horizontal obstacle speed |
| `BUTTON_PIN` / `BUZZER_PIN` | `D6` / `D5` | Input and sound pins |

The melody and note definitions are in `song.h`.

## Validation and limitations

Check the OLED address, active-low button response, jump timing, collision, audio, and repeated restart on the target board. No automated tests or measured hardware performance results are included.

- Collision checks use horizontal overlap while the player is exactly at ground level, rather than full bounding-box overlap throughout a jump.
- Jump-overlap scoring can award points across multiple frames for the same obstacle.
- The game-over wait loop does not explicitly yield or delay; verify restart/watchdog behavior on the selected ESP8266 core.
- Audio uses blocking note delays, and a held button may initiate another jump after landing.
- Scores are stored in RAM and reset when restarting; there is no persistent high score.
- The sketch has no network connection or external account configuration.

## Demonstration and contributions

The original project also links to a [short hardware video](https://vt.tiktok.com/ZSjaQG491/). See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidance; there is currently no repository test or lint command.

## License

[MIT License](LICENSE). The melody header retains attribution to Robson Couto's [arduino-songs collection](https://github.com/robsoncouto/arduino-songs). Third-party libraries and reused assets remain subject to their own terms.
