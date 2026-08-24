

                                  The universal controller
                                          By Koray                                                                                                  
![image](https://raw.githubusercontent.com/koray9012/The-universal-controller/refs/heads/main/20260823_182458.jpg)
The Universal Controller is a custom-built, dual-joystick ESP32 handheld transmitter engineered for low-latency wireless hardware control via ESP-NOW. Built with real-time OLED telemetry feedback, customizable mode toggles, and fail-safe link monitoring, it acts as a modular remote platform for driving 4WD rovers and controlling their functions,

## Key Upgrades & Features
  
  • Low-Latency ESP-NOW Communication: Direct peer-to-peer 2.4 GHz wireless protocol bypassing traditional Wi-Fi router latency.

  • Bi-Directional Link Monitoring: Real-time heartbeat telemetry with visual [ONLINE] / [OFFLINE] feedback and hardware connection fail-safes.

  • Dual 2-Axis Joystick Controls: Precision analog reading with deadzone filtering, vector mapping, and cross-talk suppression.

  • OLED Status Display: 128x64 SSD1306 screen outputting real-time system modes, steering vectors, and network telemetry.

  • Multi-Mode Control Schemes: Integrated front toggles to switch between standard operational modes and raw high-speed manual overrides.

  • Status LED Indicators: Onboard diagnostic LEDs for active transmission, link status, and menu state.

  • Modular Receiver Protocol: Universal struct-based packet design for simple integration with 4WD rovers and their atachments

## How to use: 

To set up and run the system, first get the target vehicle's MAC address using a standard scanner sketch, paste it into the transmitter code's roverAddress[] array, and flash both the controller and receiver ESP32 boards. Once both units are powered on, wait a second for the controller's OLED screen to switch from [OFFLINE] to [ONLINE], confirming the bi-directional ESP-NOW link is live.

To drive, push the left joystick forward to move ahead, or tilt it left and right to steer, releasing it to automatically send a stop signal. You can use the front mode button on GPIO 25 to toggle control profiles, or press the menu button on GPIO 27 to pop up the diagnostic screen. If the vehicle ever strays out of range or loses power for over 500 milliseconds, the receiver instantly cuts motor power as an automatic fail-safe until signal returns.
Here is so clean instructions on how to do it step by step:

## Operating Instructions

Power on both the handheld controller and your receiver vehicle. The link status on the OLED screen will automatically flip from [OFFLINE] to [ONLINE] within a second, confirmed by the solid green power LED once the bi-directional ESP-NOW heartbeat connects.

Push the left joystick forward to send a continuous drive command, or deflect it left and right to steer; releasing the stick back to neutral instantly broadcasts a stop command to the motors. Use the top trigger buttons (GPIO 4 and GPIO 13) for quick acceleration or braking overrides. Press the front mode switch (GPIO 25) to cycle between control sensitivity profiles, or press the menu button (GPIO 27) to toggle the diagnostic overlay on the OLED display and turn on internal box lights. If the vehicle moves out of range or loses connection for longer than 500 milliseconds, the receiver's automatic fail-safe will kill motor power until signal is recovered.

  ## Why I made it:

I built the Universal Controller because standard RC transmitters are way too expensive, locked down, and annoying to configure for custom robotics projects. Most DIY wireless solutions either force you to set up a bloated Wi-Fi access point with terrible latency, or use basic Bluetooth setups that drop connections and give you zero feedback on what's actually happening.

I wanted one clean, reliable handheld transmitter that could control any of my hardware projects—from my custom off-grid Mars rover to future 3D-printed builds and microcontrollers. By leveraging ESP-NOW, I got near-instant peer-to-peer response times without needing a router. Adding the OLED display and a bi-directional heartbeat meant I could finally see real-time link diagnostics right in my hands instead of guessing why a motor stopped responding.
It started as a simple cliff-avoidance test, but turned into a full-on crash course in I2C multiplexing, web socket latency tuning, C++ state machines, and custom hardware integration and i plan to upgrade it constantly and one day to make it absolutely perfect.

### Wiring & Connections:

Below is the visual schematic diagram for Edge Detector 2.0.

![image](https://github.com/koray9012/Edge-detecting-robot-2.0/blob/main/%D0%95%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D0%B0%20%D1%81%D0%BD%D0%B8%D0%BC%D0%BA%D0%B0%202026-07-29%20005514.png?raw=true)

### Pinout Breakdown:

| ESP32 Pin | Component | Connected Pin / Note |
| :--- | :--- | :--- |
| **GPIO 32** | Left Joystickr | VRx (Horizontal Axis) |
| **GPIO 33** | Left Joystick | VRy (Vertical Axis) |
| **GPIO 34** | Right Joystick | VRx (Horizontal Axis) |
| **GPIO 35** | Right Joystick | VRy (Vertical Axis) |
| **GPIO 21** | OLED Display | Shared I2C SDA |
| **GPIO 22** | OLED Display | Shared I2C SCL)  |
| **GPIO 4** | L2 Top Button | Button Pin (other pin to GND) |
| **GPIO 13** | R2 Top Button | Button Pin (other pin to GND) |
| **GPIO 25** | Mode Pushbutton | Button Pin (other pin to GND) |
| **GPIO 27** | Menu Pushbutton | Button Pin (other pin to GND) |
| **GPIO 2** | TX Blue LED | LED (+) Positive (other pin GND) |
| **GPIO 17** | Power Green LED| LED (+) Positive (other pin GND) |
| **GPIO 16** | Diag White LED | LED (+) Positive (other pin GND) |
| **3.3V** | OLED + Both Joysticks | 3.3V power pin for esp32 |
| **GND** | Shared GND of all devices | Shared GND cable |


## Code:

The code can be found in repo: Universal controller code

## Bill of materials:

| Item | Quantity | Price (USD) | Link |
| :--- | :--- | :--- | :--- |
| ESP32 30 Pin Expansion Board | 1 | 8.68 USD | https://www.ardboard.com/index.php?route=product/product&product_id=413 |
| Dual 2-Axis Joystick Module | 1 | 4.60 USD | https://elimex.bg/product/74876-kit-k2125-modul-ps2-dzhoystik-za-avrpic-i-dr |
| 0.96 Oled Display | 1 | 5.60 USD | https://www.ardboard.com/index.php?route=product/product&product_id=264&search=oled |
| Pushbutton (L2, R2, Mode, Menu) | 4 | 0.12 USD x4 = 0.48 USD | https://elimex.bg/product/85908-mikrobuton-12-12-7.5-kan1211 |
| 3mm LED (Blue, Green, White) | 1 | 0.12 USD | https://elimex.bg/product/59013-led-8mm-diff-green |
| Jumper Cables | ~30 | 5.77 USD x2 = 11.54 USD | [https://elimex.bg/product/85664-akumulator-3.7v-3400mah-lc18650-lav](https://elimex.bg/product/75823-komplekt-provodnitsi-40-broya-s-konektori-mazhki-zhenski-30sm AND https://elimex.bg/product/74894-komplekt-provodnitsi-40-broya-s-konektori-mazhki-mazhki-20sm)a |
| LoRa | 1 | 0.28 USD x4 = 1.12 USD | https://www.ardboard.com/lora-ra-02-433MHz?search=LoRa |
| 18650 battery | 1 | 1.52 USD | https://elimex.bg/product/85664-akumulator-3.7v-3400mah-lc18650-lava |
| Power Switch | 1 | 0.35 USD | https://elimex.bg/product/44024-switch-smrs101-1-black | 
| TP4056 | 1 | 1.73 USD | https://elimex.bg/product/92572-kit-k645-zariadno-za-li-ion-baterii-s-usb-micro | 


## Very important: The motors came with the chasis because they are a kit and also the cables arent exacly 30 bc i cut them up and soldered them 

## Video for controller demo ()

## Credits: 

This porject uses:

Kicad

Hack Club Macondo 

Btw thank you for the pinecil Hack CLub :)
