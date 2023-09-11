**Laboratory: MQTT Communication with Python on Raspberry Pi**

**Objective:**
This laboratory session builds upon the previous session, where you installed and tested Mosquitto on a Raspberry Pi. In this session, you will create Python programs to subscribe to and publish messages to the MQTT broker running on the Raspberry Pi. Additionally, you will connect to the Raspberry Pi via SSH from your Windows or macOS command line.

**Materials:**
- Raspberry Pi 4 with Raspberry Pi OS installed and Mosquitto MQTT broker configured (as per the previous session).
- Windows or macOS computer.

**Procedure:**

**Connecting to the Raspberry Pi via SSH:**
1. **For Windows:**
    - Open the Command Prompt.
    - Use the `ssh` command to connect to your Raspberry Pi. Replace `<pi_username>` with your Raspberry Pi username and `<pi_ip>` with the Raspberry Pi's IP address.
    ```bash
    ssh <pi_username>@<pi_ip>
    ```
    
2. **For macOS:**
    - Open the Terminal.
    - Use the `ssh` command to connect to your Raspberry Pi using the same format as above.

**Python MQTT Subscriber:**
1. On the Raspberry Pi (via SSH), create and open a Python script for subscribing to MQTT messages. You can use the `nano` text editor or any other text editor you prefer.
   ```bash
   nano mqtt_subscriber.py
   ```

2. Copy and paste the following Python code into the `mqtt_subscriber.py` file. This code subscribes to an MQTT topic and displays incoming messages.
   ```python
   import paho.mqtt.client as mqtt

   # Define the MQTT broker and topic
   broker_address = "localhost"  # Replace with the Raspberry Pi's IP if not running locally
   topic = "test/topic"  # Replace with the desired MQTT topic

   # Callback functions for MQTT client
   def on_connect(client, userdata, flags, rc):
       print("Connected to MQTT broker with result code " + str(rc))
       client.subscribe(topic)

   def on_message(client, userdata, message):
       print(f"Received message on topic '{message.topic}': {message.payload.decode()}")

   # Create an MQTT client
   client = mqtt.Client()

   # Set up callback functions
   client.on_connect = on_connect
   client.on_message = on_message

   # Connect to the MQTT broker
   client.connect(broker_address)

   # Start the MQTT client loop to receive messages
   client.loop_forever()
   ```

3. Save the file and exit the text editor.

4. Run the subscriber program on the Raspberry Pi via SSH:
   ```bash
   python3 mqtt_subscriber.py
   ```

**Python MQTT Publisher:**
1. On the Raspberry Pi (via SSH), create and open a Python script for publishing MQTT messages. Use the `nano` text editor or your preferred text editor.
   ```bash
   nano mqtt_publisher.py
   ```

2. Copy and paste the following Python code into the `mqtt_publisher.py` file. This code publishes random numbers to an MQTT topic every second.
   ```python
   import paho.mqtt.publish as publish
   import random
   import time

   # Define the MQTT broker and topic
   broker_address = "localhost"  # Replace with the Raspberry Pi's IP if not running locally
   topic = "test/topic"  # Replace with the desired MQTT topic

   while True:
       try:
           # Generate a random number between 0 and 100
           random_number = random.randint(0, 100)

           # Publish the random number to the MQTT topic
           publish.single(topic, payload=str(random_number), hostname=broker_address)

           print(f"Published: {random_number}")

           # Wait for one second before publishing the next number
           time.sleep(1)
       except KeyboardInterrupt:
           print("Publishing stopped.")
           break
   ```

3. Save the file and exit the text editor.

4. Run the publisher program on the Raspberry Pi via SSH:
   ```bash
   python3 mqtt_publisher.py
   ```

**Review Questions:**
1. How did you connect to the Raspberry Pi from your Windows or macOS command line?
2. Explain the purpose of the MQTT subscriber program.
3. What is the role of the MQTT publisher program?
4. How can you modify the MQTT topic and message payload in the publisher program to suit your needs?
5. What are the key components of the MQTT Python programs you created, and what is their purpose?
6. How could these MQTT communication techniques be applied in real-world IoT projects?

Ensure you document your observations and any issues encountered during this laboratory exercise in your report.
