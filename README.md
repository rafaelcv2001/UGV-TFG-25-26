# UGV_TFG_25-26
Indoor UGV prototype based on Raspberry Pi 5. Features skid-steering, ultrasonic sensor-based obstacle avoidance, and YOLO-powered object detection. Supports manual (DualShock 4) and autonomous operation. UCA Final Degree Project 2026.

# Indoor UGV – Mechanical Engineering Final Degree Project (in progress)

> Unmanned Ground Vehicle (UGV) for navigation in a controlled indoor environment.  
> Final Degree Project — University of Cádiz, 2025–2026.

---

## What is this project?

Design and integration of a low-cost UGV for indoor environments, capable of operating in manual mode (DualShock 4) and autonomous mode (decision-making based on detected traffic signs).

The project covers the full workflow: CAD mechanical design → component selection → electronic architecture → control software development.

---

## Current status

| Phase | Status |
|------|--------|
| CAD Design | ✅ Completed |
| Electronic architecture defined | ✅ Completed |
| Manufacturing drawings | ✅ Completed |
| Control scripts (Python) | 🔄 In progress |
| Physical integration | ⏳ Pending |
| Testing and calibration | ⏳ Pending |

---

## System architecture

- **Control:** Raspberry Pi 5  
- **Manual Input:** DualShock 4 via Bluetooth  
- **Drive Unit:** Adafruit DC & Stepper Motor HAT + 4× TT motors  
- **Distance Sensors:** Ultrasonic sensors (HC-SR04)  
- **Vision:** Front camera + YOLO26  
- **Main Functions:** manual driving, autonomous mode, emergency braking  

---

## Mechanical design

The chassis and sensor mounts are modeled in **FreeCAD** (PartDesign // Assembly4), and the drawings are produced in AutoCAD using a student license.

| | |
|---|---|
| ![General view](docs/img/render_general.png) | ![Exploded view](docs/img/render_explosionado.png) |
| General view of the UGV | Exploded view of components |

| | |
|---|---|
| ![Sensor mount](docs/img/detalle_sensores.png) | ![Chassis drawing](docs/img/plano_chasis.png) |
| HC-SR04 mount detail | Chassis drawing (AutoCAD) |

> `.FCStd` files and PDF drawings available upon request (Final Degree Project currently under active submission).

---

## Main components

| Component | Model | Function |
|---|---|---|
| Onboard computer | Raspberry Pi 5 (8 GB) | Central control |
| Motor HAT | Adafruit DC & Stepper Motor Bonnet | Control of 4× TT DC motors |
| Motors | TT Motor 1:48 | Skid-steering traction |
| Front sensor (90º) | HC-SR04 | Obstacle detection – Emergency braking |
| Diagonal sensors (45º and 135º) | HC-SR04 (×2) | Obstacle detection – Emergency braking |
| Camera | RPi Camera | YOLO-based vision |
| Controller | DualShock 4 | Manual control / mode switching |

---

## Software logic

- **Manual mode:** controlled using the DualShock 4 controller.
- **Autonomous mode:** activated by holding the **Square** button.
- **Acceleration / braking:** L2 and R2 triggers.
- **Steering:** left joystick.
- **Manual lock:** **X** button.
- **Emergency braking:** ultrasonic sensors.
- **Sign detection:** vision system using YOLO.
- **Sign-based behavior:** detection and decision-making (stop, move forward, 90º left/right reorientation) according to what is observed.

**Project software stack:**
- Python 3 on Raspberry Pi 5, with process orchestration using _subprocess_.
- Powertrain control through `adafruit-circuitpython-motorkit`.
- Distance acquisition using `gpiozero`.
- DualShock 4 controller input via Bluetooth (`evdev`).
- Visual perception based on YOLO.

---

## Design decisions and documented limitations

- **Diagonal ultrasonic sensors:** mounting at 45°/135° produces specular reflections that return longer distances than the real ones. This is documented in the final report.  
  Adopted solution: ultrasonic sensors are used as obstacle alarms, not as metric references for _wall-following_. Emergency braking relies on the front ToF sensor.

- **Controlled environment:** the system is designed for indoor use with stable lighting and flat surfaces. Outdoor operation is not considered at this stage.

---

## Final Degree Project documentation

📄 [View full report (PDF)](docs/TFG_memoria.pdf) ← *(available after submission, September 2026)*

---

## Author

**Rafael Coronel Varo**  
Mechanical Engineering Degree – University of Cádiz  
📧 [rafaelcoronelvaro@gmail.com](mailto:rafaelcoronelvaro@gmail.com)  
🔗 [linkedin.com/in/rafael-coronel-varo](https://linkedin.com/in/rafael-coronel-varo)
