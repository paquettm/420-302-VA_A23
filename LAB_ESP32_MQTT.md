# Lab: MQTT on ESP32

**Part 1: Implementing an MQTT Client on ESP32**

**Objective:**
- To implement an MQTT client on an ESP32 microcontroller and establish communication with an MQTT broker.

**Materials:**
- ESP32 development board
- USB cable for programming and power
- Computer with Arduino IDE installed
- Wi-Fi network with internet access
- MQTT broker (e.g., Mosquitto) running on a local server

**Prerequisites:**
- Basic knowledge of Arduino programming.
- Understanding of MQTT and its concepts.

**Procedure:**

**Setup:**

1. **Software Installation:**
   - Make sure you have Arduino IDE installed on your computer.
   - Install the required libraries:
     - WiFi
     - PubSubClient

2. **Hardware Connection:**
   - Connect the ESP32 board to your computer using a USB cable.

**Programming:**

3. **Open Arduino IDE:**
   - Launch the Arduino IDE on your computer.

4. **Load the Code:**
   - Write the following code into the Arduino IDE:

```cpp
//libraries to integrate functionality
#include <WiFi.h> //wifi connection
#include <PubSubClient.h> //MQTT messaging
#include <Arduino.h> //Input and output

// Wi-Fi credentials: replace with those of your network
const char* ssid = "ssid";  // The name of the WiFi network
const char* password = "passkey"; // The WiFi network passkey

// MQTT broker details: replace with your own
const char* mqtt_server = "devicename.local"; // The MQTT broker's hostname or IP address
const int mqtt_port = 1883;  // MQTT broker port (1883 is default)
const char* mqtt_topic = "house/greeting";  // MQTT topic to publish messages
// MQTT client name prefix (will add MAC address)
String name = "ESP32Client_";

// Create an instance of the WiFiClient class
WiFiClient espClient;
// Create an instance of the PubSubClient class
PubSubClient client(espClient);

// Timer for publishing every 5 seconds
unsigned long previousMillis = 0;
const long interval = 5000;

void setup() {
  // Start Serial communication
  Serial.begin(115200);

  // Read the MAC address
  uint8_t mac[6];
  esp_read_mac(mac, ESP_MAC_WIFI_STA);
  // Convert MAC address to a string
  char macStr[18]; // MAC address is 12 characters long without separators, plus null terminator
  snprintf(macStr, sizeof(macStr), "%02X:%02X:%02X:%02X:%02X:%02X", mac[0], mac[1], mac[2], mac[3], mac[4], mac[5]);
  // Concatenate the name prefix with the MAC address 
  name = name + macStr;

  // Connect to Wi-Fi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");

  // Set MQTT server and port
  client.setServer(mqtt_server, mqtt_port);
}

void loop() {
  // Connect to MQTT if necessary
  if (!client.connected()) {
    connect();
  }

  // Get the current time
  unsigned long currentMillis = millis();

  // Publish a message every 5 seconds
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;

    // Your message to publish
    String message = "Hello all from " + name;

    // Publish the message to the MQTT topic
    client.publish(mqtt_topic, message.c_str());
    Serial.println("Message sent: Hello all from " + name);
  }

  // Allow the PubSubClient to process incoming messages
  client.loop();
}

void connect() {
  // Loop until we're reconnected
  while (!client.connected()) {
    Serial.println("Attempting MQTT connection...");

    // Attempt to connect
    if (client.connect(name.c_str())) {
      Serial.println("Connected to MQTT broker");
    } else {
      Serial.print("Failed to connect to MQTT broker, rc=");
      Serial.print(client.state());
      Serial.println("Try again in 5 seconds");
      delay(5000);
    }
  }
}
```

5. **Code Explanation and Comments:**

   - The code begins by including necessary libraries for Wi-Fi, MQTT, and Arduino functionality.
   - Replace the `ssid` and `passkey` strings with the credentials of your Wi-Fi network.
   - Replace the `mqtt_server` variable contents with the hostname or IP address of your MQTT broker.
   - Modify the `mqtt_topic` variable content to specify the MQTT topic you want to use.
   - The `name` variable combines a client name prefix with the ESP32's MAC address to create a unique client identifier.

6. **Upload the Code:**
   - Select your ESP32 board from the "Tools" > "Board" menu. (You probably have an `ESP32 Dev Module`)
   - Select the correct COM port under the "Tools" > "Port" menu. (The correct port probably contains "USB" in its designation if you are connected over USB)
   - Click the "Upload" button (right arrow ![Upload](Upload.png "Upload")) to upload the code to the ESP32. Note that the checkmark icon to its left is the "Compile" button which compiles but does not send the program to the device.

7. **Monitor Serial Output:**
   - Open the Serial Monitor in the Arduino IDE (Tools > Serial Monitor).
   - Ensure that the baud rate is set to 115200.
   - You should see messages indicating the ESP32's connection to Wi-Fi and MQTT broker.

**Testing:**

8. **Verify MQTT Communication:**
   - Check your MQTT broker (e.g., Mosquitto) for incoming messages on the specified topic ("house/greeting"). You should see messages published by your ESP32.

**Troubleshooting:**

9. **Debugging:**
   - If you encounter any issues, carefully review the code for errors and check your Wi-Fi and MQTT broker settings.
   - Verify that your ESP32 is connected to Wi-Fi and can reach the MQTT broker.
   - If you are having compilation errors, see the troubleshooting section lower in this document.

**Conclusion:**

10. **Completion:**
    - Congratulations! You have successfully implemented an MQTT client on an ESP32 microcontroller, allowing it to publish messages to an MQTT broker.

11. **Further Exploration:**
    - Experiment with different MQTT topics and payloads to expand your understanding of MQTT communication.

12. **Cleanup:**
    - Disconnect the ESP32 from your computer.


**Device Naming and MQTT: Ensuring Uniqueness with MAC Addresses**

When working with MQTT (Message Queuing Telemetry Transport), it is crucial to ensure that each connected device has a unique identifier or name. This unique identifier plays a significant role in identifying and managing devices within the MQTT ecosystem. One common and effective approach to achieving this uniqueness is by utilizing the MAC (Media Access Control) address of the device's network interface. Here's why unique device names are essential and why MAC addresses are a suitable choice:

**1. Avoiding Collisions:**
   - MQTT operates on a publish-subscribe messaging model where devices communicate through topics. To prevent topic collisions and ensure that messages reach the intended recipient, it is vital for each device to have a distinct name or client ID.

**2. MQTT Broker Management:**
   - MQTT brokers, such as Mosquitto, rely on unique client IDs to distinguish between different devices. These IDs allow the broker to maintain session state and route messages accurately.

**3. Scalability:**
   - In IoT (Internet of Things) and home automation scenarios, where numerous devices may connect to the MQTT broker, unique names become essential for scalability. Without uniqueness, it would be challenging to manage and control a large number of devices effectively.

**4. Security and Authorization:**
   - MQTT brokers often implement security and authorization mechanisms. Unique client IDs are a fundamental part of these security measures, allowing administrators to control access and permissions based on device identity.

**Why Use MAC Addresses:**

The MAC address of a device's network interface is an excellent candidate for generating unique names for several reasons:

**1. Inherent Uniqueness:**
   - MAC addresses are typically hardcoded into network interface hardware during manufacturing. This hardware-assigned uniqueness ensures that no two devices share the same MAC address on a given network.

**2. Device Identification:**
   - MAC addresses are unique not just within an MQTT broker but across the entire network. This makes them highly suitable for device identification, as they provide a globally unique identifier.

**3. Minimal Configuration:**
   - Using MAC addresses as device names minimizes the need for manual configuration or user intervention. Devices can generate their MQTT client IDs automatically, simplifying deployment and maintenance.

**4. Consistency:**
   - When devices use MAC addresses as client IDs, it creates a consistent and standardized naming convention, making it easier for administrators to manage and monitor devices.

**Conclusion:**

In MQTT-based applications, having unique names for devices is essential for reliable communication, scalability, and security. The MAC address, due to its inherent uniqueness and minimal configuration requirements, is an excellent choice for generating these unique identifiers. It simplifies the process of device identification, ensuring that each device in your MQTT network can be easily distinguished and managed, contributing to the overall efficiency and robustness of your IoT or messaging system.




**Part 2: Ambient Lighting Measurement and MQTT Transmission**

**Objective:**
- To measure ambient lighting using a photocell and resistor voltage divider, read the sensor values with the Arduino, and transmit the lighting data over MQTT to the "room/lighting" topic.

**Materials:**
- ESP32 development board (from Part 1)
- USB cable for programming and power (from Part 1)
- Computer with Arduino IDE installed (from Part 1)
- Wi-Fi network with internet access (from Part 1)
- MQTT broker (e.g., Mosquitto) running on a local server (from Part 1)
- 10k-ohm resistor
- Photocell (light-dependent resistor or LDR)
- Breadboard and jumper wires
- Multimeter (for calibration)

**Circuit Building Procedure:**

1. **Assemble the Circuit:**
   - Place the ESP32 development board on a breadboard.
   - Connect one leg of the photocell to one terminal of the 10k-ohm resistor.
   - Connect the other leg of the photocell to the ESP32's VCC pin (e.g., A0).
   - Connect the other terminal of the resistor to the ESP32's ground (GND) pin.
   - Connect a jumper wire from the junction of the photocell and resistor a usable ESP32 analog input pin, e.g., GPIO34 as used in the code below.

   Your circuit should resemble a voltage divider, with the photocell and resistor connected in series between 3.3V and GND, and the junction connected to the ESP32's analog pin.

   Notes:

   - Consult the pinout for your board to know the exact pinout. GPIO pin numbers (logical) are used in the code, not physical (sequential from 1 to ...) pin numbers. E.g., [for ESP-WROOM-32](https://randomnerdtutorials.com/esp32-adc-analog-read-arduino-ide/).
   - ESP32 ADC2 pins cannot be used when Wi-Fi is used. So, if you’re using Wi-Fi and you’re having trouble getting the value from an ADC2 GPIO, you may consider using an ADC1 GPIO instead, that should solve your problem.
   - The resistor value must be sufficient to limit current.
   - In the absence of a photoresistor and resistor, simulate with a potentiometer.

3. **Calibration (Optional):**
   - For accurate light measurements, calibrate the sensor in a known lighting condition (e.g., full daylight and complete darkness).
   - Use a multimeter to measure the resistance of the photocell in both conditions and note the values.
   - Use these values to map the photocell resistance to a lighting level in your Arduino code (explained in the code section).

**Code Addition:**

3. **Modify the Existing Code:**
   - Open the Arduino IDE and load the code from Part 1.

4. **Add Lighting Measurement Code:**
   - Add the following code snippet to measure the lighting level using the photocell:

```cpp
int lightPin = 34; // Analog pin connected to the photocell
int lightValue = 0; // Variable to store the light level

void setup() {
  // ... (previous setup code)

  // Configure the analog pin for input
  pinMode(lightPin, INPUT);
}

void loop() {
  // ... (previous loop code)

  // Measure the light level
  lightValue = analogRead(lightPin);

  // You may need to map the lightValue to the desired lighting range based on calibration
  // For example, if your photocell resistance values are known for full daylight and darkness, use map() function here.
  // lightValue = map(lightValue, minVal, maxVal, 0, 100); // Map to a 0-100 lighting scale

  // Publish the lighting data to the MQTT topic
  String lightingMessage = "Lighting level: " + String(lightValue);
  client.publish("room/lighting", lightingMessage.c_str());

  // ... (rest of the loop code)
}
```

   - Modify the `lightPin` variable to match the analog pin you connected the photocell to.
   - Use the `analogRead()` function to read the light level from the photocell.

5. **Calibration (Optional):**
   - If you performed calibration, use the `map()` function to map the `lightValue` to the desired lighting range based on the photocell's resistance values in your code.

6. **Upload the Modified Code:**
   - Upload the modified code to your ESP32 board.

**Testing:**

7. **Test the Ambient Lighting Measurement:**
   - Ensure that the circuit is correctly connected.
   - Open the Serial Monitor to observe the lighting level readings.
   - Verify that the ESP32 is publishing lighting data to the "room/lighting" MQTT topic.

8. **Calibration Verification (Optional):**
   - If calibration was performed, ensure that the lighting measurements match the expected values in different lighting conditions.

**Conclusion:**

9. **Completion:**
    - Congratulations! You have successfully integrated a photocell and resistor voltage divider to measure ambient lighting and transmit the data over MQTT.

10. **Further Exploration:**
    - Experiment with different lighting conditions and calibration settings to refine your measurements.

11. **Cleanup:**
    - Disconnect the ESP32 and circuit components.

**Note:** In this part, we've added code to measure lighting using the photocell and transmit the data over MQTT. Calibration is optional but can improve accuracy in measuring lighting conditions. Depending on the specific photocell and resistor used, calibration values may vary, so students should adjust the code accordingly.

## Troubleshooting

### PubSubClient library

If you're having trouble finding the `PubSubClient.h` library in the Arduino IDE on your Raspberry Pi, you might need to manually install it. Here's how you can do that:

1. **Open Arduino IDE**: Launch the Arduino IDE on your Raspberry Pi.

2. **Go to Library Manager**: Click on "Sketch" in the top menu, then select "Include Library" and click on "Manage Libraries."

3. **Search for PubSubClient**: In the Library Manager, you can search for the `PubSubClient` library in the search bar.

4. **Install PubSubClient**: Once you find the `PubSubClient` library in the list, click on the "Install" button next to it. This will download and install the library on your Raspberry Pi.

5. **Check Installation**: After installation is complete, you should see a green checkmark next to the `PubSubClient` library in the Library Manager.

6. **Verify the Library**: To make sure the library is available for your sketches, you can create a new Arduino sketch and check if you can include the `PubSubClient.h` library without any errors. You can do this by adding the following line at the beginning of your sketch:

   ```cpp
   #include <PubSubClient.h>
   ```

If you still face issues, make sure your Arduino IDE is up to date and your Raspberry Pi is connected to the internet. Occasionally, network issues can prevent the IDE from downloading and installing libraries. You can also try restarting the Arduino IDE after installing the library.

Additionally, if you have installed the Arduino IDE through Snap or another package manager, there might be some permission issues. In that case, you can try running the Arduino IDE with elevated privileges using `sudo`, but be cautious when using `sudo` with GUI applications to avoid any unintended consequences.

```bash
sudo arduino
```

Remember that using `sudo` can have security implications, so use it only if you can't resolve the issue through other means.

## Not compiling at all

Try restarting the Arduino IDE as it will clear some memory states and compilation files.
