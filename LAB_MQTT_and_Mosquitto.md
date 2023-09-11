
# Laboratory: Installing and Testing Mosquitto on Raspberry Pi

## Objective:
The objective of this laboratory session is to install and test the Mosquitto MQTT broker on a Raspberry Pi 4 running the latest Raspberry Pi OS. MQTT is a crucial protocol used in various Internet of Things (IoT) applications for efficient communication between devices.

##An overview of MQTT and Mosquitto

**MQTT (Message Queuing Telemetry Transport):**
MQTT is a lightweight, publish-subscribe messaging protocol designed for efficient communication in constrained or unreliable networks, making it well-suited for Internet of Things (IoT) applications. It was developed by IBM in the late 1990s but has gained widespread adoption due to its simplicity and efficiency.

Key concepts of MQTT:
- **Publish-Subscribe Model:** MQTT uses a publish-subscribe pattern where devices communicate through a central broker. A central broker is a server with a set IP address which all authenticated devices can access. Devices can publish messages to specific "topics," and other devices interested in those topics can subscribe to receive messages published to them.

- **Quality of Service (QoS):** MQTT supports three levels of QoS:
  1. QoS 0 (At most once): Messages are delivered once or not at all. This level offers the least reliability.
  2. QoS 1 (At least once): Messages are guaranteed to be delivered at least once. This level ensures message delivery but may lead to duplicates.
  3. QoS 2 (Exactly once): Messages are guaranteed to be delivered exactly once. This level ensures message delivery without duplicates but involves more overhead.

- **Retained Messages:** MQTT allows brokers to retain the last message sent on a topic. When a new subscriber joins, it immediately receives the retained message, providing current status information.

- **Last Will and Testament (LWT):** MQTT clients can set a "last will" message that the broker will publish on their behalf if the client unexpectedly disconnects. This is useful for detecting when devices go offline.

**Mosquitto:**
Mosquitto is an open-source MQTT broker (server) and client implementation. It is widely used for setting up MQTT broker services on various platforms, including Raspberry Pi, and plays a critical role in managing MQTT communication in IoT projects.

Key features of Mosquitto:

- **Publish-Subscribe Broker:** Mosquitto acts as a broker that facilitates the communication between MQTT clients. It accepts incoming MQTT messages from publishers and forwards them to subscribers based on the specified topics.

- **Lightweight:** Mosquitto is designed to be lightweight, making it suitable for resource-constrained devices and embedded systems.

- **Security:** Mosquitto supports various authentication mechanisms and can be configured to use SSL/TLS encryption for secure communication. This is crucial when handling sensitive data in IoT applications.

- **Bridge Functionality:** Mosquitto can be configured as a bridge to connect multiple MQTT brokers, allowing for scalable and distributed MQTT networks.

- **Persistence:** It can be configured to retain messages, enabling subscribers to receive the last known message even if they weren't connected when the message was published.

In summary, MQTT is a messaging protocol designed for efficient and reliable communication in IoT and other applications. Mosquitto is a popular MQTT broker implementation that enables the establishment and management of MQTT communication networks, making it a valuable tool in IoT development.


## Lab procedure

**Materials:**
- Raspberry Pi 4 with the latest Raspberry Pi OS installed
- Internet connection
- Terminal or SSH access to the Raspberry Pi

**Procedure:**

**Step 1: Update and Upgrade**
1.1. Open a terminal on your Raspberry Pi.

1.2. Ensure the operating system is up to date by executing the following commands:
```bash
sudo apt update
sudo apt upgrade
```

**Step 2: Installation of Mosquitto**
2.1. Install the Mosquitto MQTT broker and client tools by using the following command:
```bash
sudo apt install mosquitto mosquitto-clients
```

**Step 3: Enabling and Starting Mosquitto**
3.1. Enable Mosquitto to start on boot with this command:
```bash
sudo systemctl enable mosquitto
```

3.2. Start the Mosquitto broker service:
```bash
sudo systemctl start mosquitto
```

3.3. Verify that Mosquitto is running without errors:
```bash
sudo systemctl status mosquitto
```

**Step 4: Testing Mosquitto**
4.1. Open two terminal windows or SSH sessions, one for subscribing and one for publishing MQTT messages.

**Publishing Test:**
4.2. In one terminal, use the `mosquitto_pub` command to publish a test message to a topic. Replace `test/topic` with your chosen topic and `"Hello, MQTT!"` with your message:
```bash
mosquitto_pub -t "test/topic" -m "Hello, MQTT!"
```

**Subscribing Test:**
4.3. In the other terminal, subscribe to the same topic using the `mosquitto_sub` command:
```bash
mosquitto_sub -t "test/topic"
```

4.4. Observe the message received in the subscribing terminal.

5. Further experimentation

The `mosquitto_sub` and `mosquitto_pub` commands can be used to connect to and interact with MQTT brokers that are not running locally on your device, often referred to as "remote" brokers. MQTT is designed to be a standardized protocol, so as long as the broker you're connecting to supports the MQTT protocol (which is the case for most MQTT brokers), you can use these command-line tools to publish and subscribe to topics on remote brokers.

Here's how you can use them to connect to a remote MQTT broker:

**Subscribing to a Remote Broker:**

```bash
mosquitto_sub -h <broker_host> -p <broker_port> -t <topic>
```

- `<broker_host>`: Replace this with the hostname or IP address of the remote MQTT broker.
- `<broker_port>`: Specify the port on which the MQTT broker is listening. The default MQTT port is 1883 for non-encrypted connections and 8883 for encrypted connections (MQTT over TLS/SSL).
- `<topic>`: Set the topic to which you want to subscribe on the remote broker.

**Publishing to a Remote Broker:**

```bash
mosquitto_pub -h <broker_host> -p <broker_port> -t <topic> -m <message>
```

- `<broker_host>`: Same as above, specify the hostname or IP address of the remote MQTT broker.
- `<broker_port>`: Specify the port the MQTT broker is using.
- `<topic>`: Set the topic to which you want to publish a message on the remote broker.
- `<message>`: The message you want to publish.

Ensure you have the necessary permissions and access to the remote MQTT broker, and ensure that the broker's security settings (if any) are configured to allow your connections.

Remember to replace `<broker_host>`, `<broker_port>`, `<topic>`, and `<message>` with the specific values for the MQTT broker you intend to use.


**Review Questions:**
1. What is the primary purpose of the MQTT protocol in IoT applications?
2. How do you ensure that Mosquitto starts automatically when the Raspberry Pi boots up?
3. Explain the difference between the `mosquitto_pub` and `mosquitto_sub` commands.
4. What is the significance of the topic when publishing and subscribing to MQTT messages?
5. In what scenarios can MQTT be particularly useful in electronics and IoT projects?
6. How would you secure MQTT communication in a real-world IoT application?
