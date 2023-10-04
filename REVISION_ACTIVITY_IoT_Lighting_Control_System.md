# Revision Activity: IoT Lighting Control System Using Raspberry Pi, ESP32, and MQTT

## Instructions

In this activity, you will create an IoT lighting control system using a Raspberry Pi, an ESP32, and MQTT (Message Queuing Telemetry Transport) communication.
This project will allow you to review the material and techniques practiced to date in this course as well as gain further hands-on experience with IoT devices and their integration into a practical application.
All of the tasks listed below have been covered in class in at least one of your labs; now we are putting it all together.

## Activity Tasks

### 1. Setting Up the Raspberry Pi
You probably did this already, but in case you missed a step, don't forget to perform the following tasks for this activity.
   - Make the Raspberry Pi accessible through SSH.
   - Connect your Raspberry Pi device to a Wi-Fi network such as our `iot_wireless` network.
   - Install and configure the Mosquitto MQTT message broker on your Raspberry Pi. Configure it such that it can accept incoming connections from other devices.

### 2. Configuring the ESP32
Using Arduino IDE, make sure that your ESP32 device is programmed to perform the following operations:
   - Connect to the same Wi-Fi network as the Raspberry Pi.
   - Publish light intensity readings to an MQTT topic called "room/lighting."

Not that you must also set up a photoresistor/resistor voltage splitter circuit to obtain a voltage to read and connect the proper circuit terminal to an available ESP32 GPIO pin.

### 3. Writing Python Program for Raspberry Pi
   - Your main task is to create a Python program that will run on the Raspberry Pi. This program should:
     - Subscribe to the "room/lighting" MQTT topic.
     - Receive and process incoming light intensity readings.
     - Compare the received light level to a predefined setpoint lighting value.
     - Control a LED connected to an available GPIO pin on the Raspberry Pi based on the comparison: turn the LED on (off) if the lighting is less (equal to or more) than the setpoint.

### 4. Testing and Demonstration
   - Test your IoT lighting control system thoroughly. Try adjusting the light intensity readings and observe how the LED responds.
   - Prepare to demonstrate your functioning system to your instructor. 

### 5. Documentation and Report
   - Document your project comprehensively to a private GitHub repository and invite your prof as a collaborator. Your documentation should include:
     - The Python code for your Raspberry Pi program.
     - The Arduino C++ code folder (the one that contains the .ino file)
     - Pictures of each circuit and an overall system picture.
     - A 10-second video of the system functioning.
     - In a README.md file: An overview of the hardware components used with hyperlinks to each picture and to the video. Include one paragraph each:
       - Voltage splitter
       - ESP32 wiring
       - LED circuit
       - A description of how MQTT communication works in your system.
       - Reflect on any challenges you encountered and the solutions you implemented.
       - Reflect on the practical applications of your IoT system.
       - Reflect on the potential consequences of a malicious agent sending false MQTT room lighting readings within our system.

Note: to write the README.md document properly, refer to this [Markdown Cheatsheet](Markdown_Cheatsheet.md) which explaind basic items that you can include in your text to get a nice report.

## Grading Criteria

This activity is ungraded. However its quality can be measured using the following criteria:

- Successful setup of the Raspberry Pi and Mosquitto broker including connectivity from an external device.
- Proper programming and functionality of the ESP32 for publishing light intensity readings. This can be validated using `mosquitto_sub -t room/lighting` at the Raspberry Pi command prompt.
- Correct implementation of the Python program on the Raspberry Pi. This can be validated by the system reacting as expected given MQTT communication is properly implemented.
- Quality and completeness of your documentation and report.

**Have fun!**
