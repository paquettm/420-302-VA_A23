# Lab: Communicating with I2C Devices on Raspberry Pi in Object-Oriented Python

## Objective:
In this lab, you will learn how to enable the I2C interface on your Raspberry Pi, connect an I2C temperature sensor, and write a Python program to communicate with the sensor and read temperature data.

### Prerequisites:
- Raspberry Pi running Raspberry Pi OS (Raspbian)
- An I2C temperature sensor (e.g., MCP9808)
- Jumper wires

### Step 1: Enable I2C Interface

1.1. Open a terminal on your Raspberry Pi.

1.2. Run the following command to launch the Raspberry Pi Configuration tool:
   
   ```bash
   sudo raspi-config
   ```

1.3. Navigate to "Interfacing Options" and select "I2C."

1.4. When prompted, select "Yes" to enable the I2C interface.

1.5. Reboot your Raspberry Pi to apply the changes.

### Step 2: Connect the I2C Device

2.1. **Physical Connections**:
   - Connect the SDA (Serial Data) pin of the I2C sensor to GPIO pin 3 (physical pin 5) on your Raspberry Pi.
   - Connect the SCL (Serial Clock) pin of the I2C sensor to GPIO pin 5 (physical pin 3) on your Raspberry Pi.
   - Ensure that your Raspberry Pi and I2C sensor share a common ground connection.

2.2 **Test I2C Connection**
Open a terminal on your Raspberry Pi.

Test the I2C connection to verify that your Raspberry Pi can detect the I2C sensor using the i2cdetect command. Run the following command:

```bash
sudo i2cdetect -y 1
```

This command will display a grid showing detected I2C device addresses. Ensure that your I2C sensor's address appears in the grid, indicating a successful connection. If it doesn't, double-check your connections and address settings.

### Step 3: Install the SMBus Library

3.1. Open a terminal on your Raspberry Pi.

3.2. Install the `smbus` library using pip3:

   ```bash
   sudo pip3 install smbus
   ```

   This library allows Python to communicate with I2C devices.

### Step 4: Write Python Code to Read Temperature

4.1. Create a Python script (e.g., `temperature_sensor.py`) using your preferred text editor. You can use the `nano` text editor:

   ```bash
   nano temperature_sensor.py
   ```

4.2. Read, understand and write the following Python code into the script:

   ```python
import smbus
import time

class TemperatureSensor:
    def __init__(self, i2c_bus, i2c_address):
        # Constructor to initialize the sensor with I2C bus and address
        self.i2c_bus = i2c_bus
        self.i2c_address = i2c_address

    def get_temperature(self):
        # Method to convert temperature data from the I2C sensor
        data = self._read_sensor_data()
        temperature = ((data[0] & 0x0F) << 8) | data[1]
        temperature /= 16.0
        return temperature

    def _read_sensor_data(self):
        # Private method to read sensor data from the I2C device
        try:
            bus = smbus.SMBus(self.i2c_bus)
            # Read temperature data from the specified I2C address
            # In the datasheet for MCP9808, the temperature is stored in the
            # 0x5 register
            data = bus.read_i2c_block_data(self.i2c_address, 0x5, 2)
            return data
        except Exception as e:
            print(f"Error reading data from I2C sensor: {e}")
            return None

# I2C bus 1 is on SDA SCL pins 3,5 (physical)
i2c_bus_number = 1
# MCP9808 has a default I2C address of 0x18 (from the datasheet)
i2c_device_address = 0x18
# Creating a TemperatureSensor instance with I2C configuration
sensor = TemperatureSensor(i2c_bus=i2c_bus_number, i2c_address=i2c_device_address)
# Invoking the get_temperature method and displaying the result

while True:
    print(f"Temperature: {sensor.get_temperature():.2f}°C")
    time.sleep(1)
   ```

4.3. Save the script and exit the text editor.


## Introduction to Object-Oriented Programming (OOP)
### Object-Oriented Programming (OOP):

OOP is a programming paradigm that models real-world entities as objects with attributes and behaviors.
Objects are instances of classes, which define their attributes (data) and methods (functions).
Key OOP concepts include encapsulation, inheritance, and polymorphism.

### Explaining the Python Code:

The provided Python code demonstrates OOP principles:

TemperatureSensor is a class representing the I2C temperature sensor.
Th following instruction
```
sensor = TemperatureSensor(i2c_bus=i2c_bus_number, i2c_address=i2c_device_address)
```
creates an object, called `sensor, of th class `TemperatureSensor`.
When the object is created, we pass in configurations allowing us to interface with an actual temperature sensor.
If there were multiple temperature sensors with which to interface in our application, when we could instantiate many objects, each with their own parameters.
For example, we could have a sensor at address 0x18, another at 0x19, etc.

In class `TemperatureSensor`

- The __init__ method initializes the object. This type of function is called a `constructor`.
- The get_temperature method retrieves temperature data, converts it to a usable reading in degrees celcius and returns it.
- The _read_sensor_data method reads data from the I2C sensor.

Attributes:
- i2c_bus and i2c_address are attributes storing I2C configuration.
- in the class definition, they are preceded by the keyword `self` to make it clear that they are object attributes and not global variables.


### Step 5: Run the Python Program

5.1. Run the Python script to read temperature data from the I2C sensor:

   ```bash
   python3 temperature_sensor.py
   ```

   The script will continuously display temperature readings in degrees Celsius.

### Step 6: Observations

6.1. Observe the temperature readings displayed in the terminal. The program should read and display the temperature from your I2C temperature sensor.

6.2. Experiment with different conditions to see how the temperature readings change.

### Conclusion:
In this lab, you learned how to enable the I2C interface on your Raspberry Pi, connect an I2C temperature sensor, and use Python to communicate with the sensor and read temperature data. This skill is essential for working with various I2C-based sensors and devices in your Raspberry Pi projects.

Moreover, you were able to observe code structured usng the Object-Oriented Programming approach.
This programming paradigm enables programmers to organize code in a way that is scalable and maintainable.

### Challenge

With what you have learned so far, combine code from the current lab with code from previous labs to build 2 Python programs:

1. A Python program that reads the temperature from the i2c bus and publishes it to MQTT topic "room/temperature".
2. A Python program that subscribes to the "room/temperature" topic and outputs the data to the console, non-stop.

### Challenge 2

Using 2 objects, get readings from 2 sensors on the i2c bus and proceed as above, on topics "room1/temperature" and "room2/temperature".
