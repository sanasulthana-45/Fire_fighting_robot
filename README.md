::: {align="center"}
# 🔥 Automatic Fire Fighting Robot

### 🤖 Detect the Fire. Move Toward It. Spray Water.

An Arduino-based firefighting robot that detects a flame, turns or moves
toward its direction, and activates a water pump to spray water. It uses
flame sensors, an L298N motor driver, a servo motor, and a relay module
to demonstrate a simple automatic fire-response system.

![Arduino](https://img.shields.io/badge/Controller-Arduino%20Uno-blue?style=for-the-badge&logo=arduino&logoColor=white)
![C++](https://img.shields.io/badge/Code-Arduino%20C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Sensors](https://img.shields.io/badge/Sensing-Flame%20Sensors-orange?style=for-the-badge)
![Project](https://img.shields.io/badge/Project-Robotics-red?style=for-the-badge)

**Automatic Detection • Directional Movement • Water Spraying**
:::

------------------------------------------------------------------------

## 📑 Table of Contents

-   [🌟 About the Project](#-about-the-project)
-   [✨ Features](#-features)
-   [🛠️ Components Required](#️-components-required)
-   [🧠 System Architecture](#-system-architecture)
-   [⚙️ How It Works](#️-how-it-works)
-   [🔌 Pin Connections](#-pin-connections)
-   [📚 Software and Libraries](#-software-and-libraries)
-   [🚀 Getting Started](#-getting-started)
-   [🧪 Testing the Robot](#-testing-the-robot)
-   [✅ Project Result](#-project-result)
-   [🔮 Future Improvements](#-future-improvements)
-   [⚠️ Safety Precautions](#️-safety-precautions)

------------------------------------------------------------------------

## 🌟 About the Project

The **Automatic Fire Fighting Robot** is designed to detect a flame and
respond without requiring manual control. Three flame-sensor inputs are
used to estimate whether the flame is on the left, in the center, or on
the right. An Arduino Uno processes the sensor readings and controls the
drive motors, servo-mounted water outlet, and water pump.

The L298N motor driver controls the robot's movement. A relay switches
the water pump, while a servo motor changes the direction of the water
outlet.

🎯 **Project goal:** Demonstrate how sensors, a microcontroller, and
actuators can work together to detect a flame and initiate a basic
firefighting response.

> **Important:** This is an educational prototype. It is not a
> replacement for certified fire alarms, fire extinguishers, or
> professional firefighting equipment.

## ✨ Features

  -----------------------------------------------------------------------
  Feature                             Description
  ----------------------------------- -----------------------------------
  🔥 Flame Detection                  Reads three flame-sensor inputs

  ↩️ Direction Detection              Compares readings to estimate left,
                                      center, or right

  🚗 Motor Control                    Uses an L298N driver to control the
                                      drive motors

  💧 Automatic Water Pump             Switches the pump through a relay
                                      module

  🎯 Servo Nozzle Direction           Turns the water outlet toward the
                                      detected direction

  🖥️ Serial Monitoring                Displays sensor values and
                                      detection status in Serial Monitor

  🤖 Automatic Operation              Responds to sensor readings in the
                                      Arduino program
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 🛠️ Components Required

  -----------------------------------------------------------------------
  Component                           Purpose
  ----------------------------------- -----------------------------------
  Arduino Uno                         Reads sensors and controls the
                                      system

  3 flame sensor modules with analog  Detect flame direction
  outputs                             

  L298N motor driver                  Drives the robot's DC motors

  DC geared motors and robot chassis  Move the robot

  Servo motor                         Aims or sweeps the water outlet

  Relay module                        Switches the water pump on and off

  DC water pump and tubing/nozzle     Delivers water toward the target

  Suitable battery/power supplies     Power the controller and
                                      motors/pump as required

  Jumper wires and connectors         Make electrical connections
  -----------------------------------------------------------------------

*Use the voltage and current ratings specified by each component. The
exact battery arrangement depends on the motors, pump, and modules
used.*

## 🧠 System Architecture

The following diagram shows the main control path:

``` mermaid
flowchart TD
    A["🔥 Left, Center and Right Flame Sensors"] --> B["⚡ Arduino Uno"]
    B --> C["🚗 L298N Motor Driver"]
    C --> D["DC Drive Motors"]
    B --> E["🎯 Servo Motor"]
    E --> F["Water Outlet / Nozzle"]
    B --> G["🔌 Relay Module"]
    G --> H["💧 Water Pump"]
    H --> F
    B --> I["🖥️ Serial Monitor"]
```

### ⚙️ How It Works

1.  **Read sensors:** The Arduino reads the analog values from the left,
    center, and right flame sensors.
2.  **Check for a flame:** The program compares the readings with a
    threshold value of `900`. In this code, a lower reading indicates a
    stronger flame indication.
3.  **No flame detected:** If all three readings are at or above the
    threshold, the robot stops, the pump is switched off, and the servo
    returns to the center position.
4.  **Flame on the left:** The robot turns left, the pump is switched
    on, and the servo points the nozzle to approximately `45°`.
5.  **Flame on the right:** The robot turns right, the pump is switched
    on, and the servo points the nozzle to approximately `135°`.
6.  **Flame in the center:** The robot moves forward, the pump is
    switched on, and the servo sweeps the nozzle between approximately
    `60°` and `120°`.
7.  **Monitor readings:** Sensor values and detection messages are
    printed in the Serial Monitor at `9600` baud.

The sensor threshold and servo angles may need adjustment for the actual
sensors, mounting positions, servo linkage, and testing environment.

------------------------------------------------------------------------

## 🔌 Pin Connections

The table below follows the supplied `fire_fighting_robot.ino` program.
Check each module's labels and your actual wiring before applying power.

### L298N Motor Driver

  L298N Pin     Arduino Uno Pin Function
  ----------- ----------------- ---------------------------------------
  ENA                       D10 Speed control for motor channel A
  IN1                        D9 Direction control for motor channel A
  IN2                        D8 Direction control for motor channel A
  ENB                        D5 Speed control for motor channel B
  IN3                        D7 Direction control for motor channel B
  IN4                        D6 Direction control for motor channel B

### Flame Sensors, Relay, and Servo

  Component Signal                      Arduino Uno Pin Function
  ----------------------------------- ----------------- --------------------------
  Left flame sensor analog output                    A0 Left-side flame reading
  Center flame sensor analog output                  A1 Center flame reading
  Right flame sensor analog output                   A2 Right-side flame reading
  Relay control input                                D4 Switches the pump
  Servo signal                                       D3 Sets nozzle direction

**Power and ground:** Connect module grounds together where required,
and follow the electrical requirements of the specific modules. Do not
power a high-current pump or motor directly from an Arduino I/O pin. Use
an appropriate supply and driver/relay arrangement.

------------------------------------------------------------------------

## 📚 Software and Libraries

  Software / Library          Purpose
  --------------------------- ----------------------------------------------------
  Arduino IDE                 Edit and upload the program
  Arduino Uno board support   Compiles and uploads code for the Uno
  `Servo.h`                   Controls the servo motor
  `analogRead()`              Reads analog flame-sensor values
  `analogWrite()`             Sets motor-driver enable signals for speed control
  `digitalWrite()`            Sets motor direction and relay state
  `Serial`                    Prints sensor readings and status messages

The `Servo` library is included with common Arduino IDE installations.
If it is not available, install the appropriate Servo library through
the Arduino IDE Library Manager.

## 🚀 Getting Started

### 1️⃣ Assemble the Hardware

Mount the Arduino Uno, motor driver, sensors, servo, relay, pump, and
water outlet securely on the chassis. Position the flame sensors so that
they can distinguish left, center, and right directions.

### 2️⃣ Check the Connections

Wire the components according to the pin tables and your circuit
diagram. Confirm polarity, common ground requirements, supply voltage,
and current ratings before powering the robot.

### 3️⃣ Open the Program

Open `fire_fighting_robot.ino` in Arduino IDE. Confirm that the pin
definitions match your actual wiring.

### 4️⃣ Select the Board and Port

Connect the Arduino Uno to your computer. In Arduino IDE, select
**Arduino Uno** and the correct serial port.

### 5️⃣ Upload the Code

Compile and upload the sketch. Open **Serial Monitor** and set the baud
rate to **9600** to view the sensor values and status messages.

### 6️⃣ Calibrate the Sensors

Observe the readings with no flame and with a safe, controlled
flame-sensor test source. Adjust `fireThreshold` if necessary. Keep the
test source small and supervised, and do not use a real fire as a casual
test.

### 7️⃣ Test the Movement and Water System

First test the motors with the pump disconnected or disabled. Then test
the servo's direction. Finally, test the pump with water in a controlled
area, keeping electronics dry.

------------------------------------------------------------------------

## 🧪 Testing the Robot

  -----------------------------------------------------------------------
  Test Condition                      Expected Program Response
  ----------------------------------- -----------------------------------
  All sensor readings are `>= 900`    Motors stop, pump turns off, servo
                                      centers

  Left sensor is below threshold and  Robot turns left, pump turns on,
  has the lowest reading              servo moves to about `45°`

  Right sensor is below threshold and Robot turns right, pump turns on,
  has the lowest reading              servo moves to about `135°`

  Center sensor is below threshold    Robot moves forward, pump turns on,
                                      servo sweeps from about `60°` to
                                      `120°` and back

  Serial Monitor is open at 9600 baud Sensor values and status messages
                                      appear
  -----------------------------------------------------------------------

*Actual behavior depends on sensor calibration, ambient light, flame
distance, wiring, and the physical direction of the motors and servo.*

## ✅ Project Result

The project demonstrates a basic automatic firefighting response using
an Arduino Uno. Flame-sensor readings guide the robot's movement, the
relay controls the water pump, and the servo aims or sweeps the water
outlet. The prototype illustrates the integration of sensors, embedded
programming, motor control, and water delivery in a robotics project.

## 🔮 Future Improvements

-   Add obstacle detection to help prevent collisions.
-   Add a rechargeable battery system with suitable protection and power
    regulation.
-   Improve flame-direction detection through calibration and filtering.
-   Add a water-level sensor to detect an empty tank.
-   Add a manual emergency stop and pump timeout.
-   Add wireless monitoring or alerts.
-   Improve the chassis and nozzle mounting for more stable movement and
    water delivery.

## ⚠️ Safety Precautions

-   This prototype is for supervised educational demonstrations only; do
    not rely on it to fight real fires.
-   Test only in a controlled environment with a responsible supervisor
    and suitable fire-safety equipment nearby.
-   Keep the Arduino, driver, relay, battery connections, and other
    electronics protected from water.
-   Use a power supply rated for the pump and motors. Do not draw pump
    or motor current from Arduino GPIO pins.
-   Verify relay contact ratings and wiring before connecting any load.
    If using mains-powered appliances, have a qualified person handle
    the wiring; low-voltage DC testing is safer.
-   Disconnect power before changing wiring, and stop testing if wires,
    batteries, or components become hot.
-   Keep water away from mains electricity and never spray water on an
    electrical fire.

------------------------------------------------------------------------

::: {align="center"}
### 🔥 Built with Arduino \| Powered by Robotics

**Detect the flame. Aim the nozzle. Demonstrate safer automation.** 🤖
:::
