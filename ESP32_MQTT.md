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
   - Copy and paste the following code into the Arduino IDE:

```cpp
#include <WiFi.h>
#include <PubSubClient.h>
#include <Arduino.h>

// Replace with your Wi-Fi credentials
const char* ssid = "iot_wireless";  // The name of the WiFi network
const char* password = "Unsecure!"; // The WiFi network passkey

// MQTT broker details
const char* mqtt_server = "paquette-pi4.local"; // The MQTT broker's hostname or IP address
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
   - Replace the `ssid` and `password` variables with the credentials of your Wi-Fi network.
   - Replace the `mqtt_server` variable with the hostname or IP address of your MQTT broker.
   - Modify the `mqtt_topic` variable to specify the MQTT topic you want to use.
   - The `name` variable combines a client name prefix with the ESP32's MAC address to create a unique client identifier.

6. **Upload the Code:**
   - Select your ESP32 board from the "Tools" > "Board" menu.
   - Select the correct COM port under the "Tools" > "Port" menu.
   - Click the "Upload" button (right arrow) to upload the code to the ESP32.

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

**Conclusion:**

10. **Completion:**
    - Congratulations! You have successfully implemented an MQTT client on an ESP32 microcontroller, allowing it to publish messages to an MQTT broker.

11. **Further Exploration:**
    - Experiment with different MQTT topics and payloads to expand your understanding of MQTT communication.

12. **Cleanup:**
    - Disconnect the ESP32 from your computer.

**Note:** Make sure to provide necessary support and guidance to students throughout the lab session, especially when they face issues during the setup or programming stages.



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
   - Connect the other leg of the photocell to the ESP32's analog pin (e.g., A0).
   - Connect the other terminal of the resistor to the ESP32's ground (GND) pin.
   - Connect a jumper wire from the junction of the photocell and resistor to the ESP32's 3.3V pin.

   Your circuit should resemble a voltage divider, with the photocell and resistor connected in series between 3.3V and GND, and the junction connected to the ESP32's analog pin.

2. **Calibration (Optional):**
   - For accurate light measurements, calibrate the sensor in a known lighting condition (e.g., full daylight and complete darkness).
   - Use a multimeter to measure the resistance of the photocell in both conditions and note the values.
   - Use these values to map the photocell resistance to a lighting level in your Arduino code (explained in the code section).

**Code Addition:**

3. **Modify the Existing Code:**
   - Open the Arduino IDE and load the code from Part 1.

4. **Add Lighting Measurement Code:**
   - Add the following code snippet to measure the lighting level using the photocell:

```cpp
int lightPin = A0; // Analog pin connected to the photocell
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
