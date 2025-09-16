# Health-Box
A smart health monitoring system that measures **body temperature** and **pulse rate**, displays them on an LCD screen, and uploads data to **ThingSpeak** for IoT-based tracking.

## Features
- Reads **body temperature** using an infrared temperature sensor.  
- Monitors **pulse rate** using a pulse sensor.  
- Displays results on a **16x2 LCD screen**.  
- Sends data to **ThingSpeak** for remote monitoring and analysis.  
- Built with **ESP32** (or Arduino).

## Components Used
- ESP32 
- MLX90614 Infrared Temperature Sensor 
- Pulse Sensor  
- 16x2 LCD Display with I2C module  
- Jumper wires & breadboard  
- Power supply USB and or battery

# Bill of Materials (BOM)

| Item No. | Component                           | Quantity | Description |
|----------|--------------------------------------|----------|-------------|
| 1        | ESP32 Development Board             | 1        | Main microcontroller for processing and IoT connectivity |
| 2        | MLX90614 Infrared Temperature Sensor | 1        | Non-contact sensor for measuring body temperature |
| 3        | Pulse Sensor                        | 1        | Optical heart rate sensor for BPM measurement |
| 4        | 16x2 LCD Display with I2C Module    | 1        | For displaying temperature and pulse readings |
| 5        | Breadboard                          | 1        | For prototyping and wiring connections |
| 6        | Jumper Wires (Male-to-Male/Female)  | ~20      | For electrical connections between components |
| 7        | USB Cable                           | 1        | For programming and powering the ESP32 |
| 8        | Power Supply (5V adapter or battery pack) | 1 | Provides power to the system |
| 9        | Resistors (various, if required)    | As needed | For signal conditioning or pull-up/pull-down |
| 10       | Enclosure/Box (optional)            | 1        | To house the health box neatly |

*Optional additions*  
- On/Off Switch  
- PCB (custom) for a permanent build  
- LEDs for status indicators

## Software & Libraries Used

### Software / Tools
- **Arduino IDE** – for coding and uploading programs to the ESP32  
- **ThingSpeak** – IoT platform for storing and visualizing health data  
- **Onshape (optional)** – for designing the physical enclosure  

### Arduino Libraries
- **Adafruit_MLX90614** – to interface with the MLX90614 infrared temperature sensor  
- **LiquidCrystal_I2C** – to control the 16x2 LCD display via I2C communication  
- **PulseSensorPlayground** (or equivalent) – for reading pulse/heart rate data  
- **WiFi.h** – to connect the ESP32 to Wi-Fi  
- **ThingSpeak.h** – to send sensor data to the ThingSpeak cloud

## Circuit Connections

### ESP32 Pin Connections

| Component                 | Pin on ESP32   | Notes |
|---------------------------|----------------|-------|
| **MLX90614 Temperature Sensor** | SDA → GPIO 21  | I²C Data line |
|                           | SCL → GPIO 22  | I²C Clock line |
|                           | VCC → 3.3V     | Power supply |
|                           | GND → GND      | Ground |
| **Pulse Sensor**          | Signal → GPIO 34 | Use an ADC-capable pin |
|                           | VCC → 3.3V     | Power supply |
|                           | GND → GND      | Ground |
| **16x2 LCD (with I2C module)** | SDA → GPIO 21 | Shared with MLX90614 (I²C bus) |
|                           | SCL → GPIO 22 | Shared with MLX90614 (I²C bus) |
|                           | VCC → 5V (or 3.3V if supported) | Power supply |
|                           | GND → GND      | Ground |

### Notes
- Both the **MLX90614** and **LCD I2C** use the **same I²C bus** (SDA: GPIO 21, SCL: GPIO 22).  
- The **Pulse Sensor** must be connected to an **ADC pin** on the ESP32 (e.g., GPIO 34, 35, or 32).  
- Ensure common **ground (GND)** between all components.  
- Use resistors or capacitors for noise reduction if the pulse readings are unstable.

## Code Overview

The Health Box code is written in **Arduino C/C++** and runs on the ESP32.  
It follows a modular structure to handle sensors, display, and IoT updates.

### Main Sections of the Code
1. **Library Imports**  
   - Includes all necessary libraries (`Adafruit_MLX90614`, `LiquidCrystal_I2C`, `PulseSensorPlayground`, `WiFi`, `ThingSpeak`).

2. **Configuration & Setup**  
   - Defines I²C pins (SDA, SCL) for the MLX90614 and LCD.  
   - Defines the pulse sensor pin (ADC input).  
   - Connects ESP32 to Wi-Fi and initializes ThingSpeak channel.  
   - Initializes LCD and sensors.

3. **Loop Function**  
   - Reads temperature from the **MLX90614 sensor**.  
   - Reads pulse/heart rate from the **Pulse Sensor**.  
   - Displays both values on the **LCD (16x2)**.  
   - Prints data to the **Serial Monitor** for debugging.  
   - Uploads data to **ThingSpeak** at regular intervals using `millis()` (non-blocking code).

4. **Helper Functions (optional)**  
   - Functions to process sensor data (e.g., averaging pulse values).  
   - Functions for error handling if Wi-Fi or sensors fail.

   ## Project images
   **Schematics**

    <img width="820" height="621" alt="Screenshot 2025-09-16 095024" src="https://github.com/user-attachments/assets/184a0f07-804e-4e77-a92e-c1994bd39b3a" />

    **Physical build setup**
   
    ![IMG_20250913_102950](https://github.com/user-attachments/assets/756a7cee-d2dd-44e7-90fc-01cc79d83e83)

    **ThingSpeak data**
   ![IMG-20250913-WA0002](https://github.com/user-attachments/assets/11d5c652-bbc9-4595-aa3a-6780f7991da0)

    **The data that the LCD shows**
   ![IMG-20250910-WA0004](https://github.com/user-attachments/assets/ca6cd5b3-2b56-4e36-9448-62373e57c0f0)

    **The casing of it**

   <img width="1601" height="817" alt="Screenshot 2025-09-15 085206" src="https://github.com/user-attachments/assets/ca62ea0a-f92e-4f4c-8c1d-aa1ee6c1e96f" />
