# IoT Assignment 2: Raspberry Pi Controller and ESP32 Sensor - Revision

This assignment is an exercise on what was done in class. You should implement this system while keeping your project in mind so that you can use what you complete her as part of your term project.

In this assignment, you will use a Raspberry Pi and an ESP32 to communicate with each other using MQTT protocol. You will also learn how to use Python to control the Raspberry Pi and read an analog signal from the ESP32.

## Requirements

- A Raspberry Pi with Python 3 installed and connected to the internet
- An ESP32 with Arduino IDE installed and connected to the computer
- A breadboard, a LED, a resistor, some jumper wires, and a potentiometer
- A configuration file named `config.json` that contains a collection of configurations consisting of conditions-results lists

## Tasks

### Task 1: The Raspberry Pi

Note: Mosquitto MQTT broker should be installed on the Raspberry Pi and ready to accept connections from outside devices.

- Write a Python program named `control.py` that does the following:
    - Reads the configuration file `config.json`
    - Subscribes to all message topics included in the configuration conditions using the `paho-mqtt` library
    - Defines a callback function that is triggered when a new message is received
    - In the callback function, checks all configurations, and if all conditions from a configuration are satisfied, publishes the MQTT messages from the results
- Write a Python program named `actor.py` that does the following:
    - Subscribes to the topic name appropriate to your project output, using the `paho-mqtt` library. For example, if you will control an aquarium heater in your project, the topic should be "aquarium/heater"
    - Defines a callback function that is triggered when a new message is received
    - In the callback function, sets the GPIO pin 18 to output mode and writes a `1` signal to it if the message payload is `on`, or a `0` signal if the message payload is `off`
    - Connects the LED and the resistor to the GPIO pin 18 and the ground pin on the Raspberry Pi using the breadboard and the jumper wires

Note: If your system will use and ESP32 as an actor instead, you may move this requirement to a second ESP32 device.

### Task 2: The ESP32

- Write an Arduino sketch named `sensor.ino` that does the following:
    - Connects to the WiFi network using the `WiFi.h` library
    - Connects to the MQTT broker on the Raspberry Pi using the `PubSubClient.h` library
    - Reads the analog signal from the potentiometer connected to the pin 34 on the ESP32
    - Maps the analog signal value to a range from 0 to 100 and publishes it to the topic name that identifies the variable you wish to measure in your project, every second. For example, if your projected system must measure aquarium water temperature, publish to "aquarium/temperature".

## Testing

- Run the `control.py` program on the Raspberry Pi
- Upload and run the `sensor.ino` sketch on the ESP32
- Run the `actor.py` program on the Raspberry Pi (or upload and run the `actor.ino` sketch on the ESP32 if this was your choice)
- Observe the LED and the messages on the MQTT broker
- Change the configuration file `config.json` to use different conditions and results
- Test if the LED behaves as expected according to the configuration file

## Submission

On GitHub
- Submit your Python and Arduino code files along with the configuration file `config.json`
- Submit a report that explains your code and the results of your testing
- Submit a video that demonstrates your IoT system in action
- Invite the teacher (GitHub account paquettm) as a contributor

Deadline November 23, 2023, 11:55PM.
