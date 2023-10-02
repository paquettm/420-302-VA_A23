# Arduino IDE & ESP8266

To install ESP8266 support and its dependencies in the Arduino IDE, follow these steps:

1. **Install the Arduino IDE:**
   If you haven't already, download and install the Arduino IDE from the official website (https://www.arduino.cc/en/software).

2. **Open Arduino IDE:**
   Launch the Arduino IDE on your computer.

3. **Add ESP8266 Board Support:**
   To program ESP8266 boards with the Arduino IDE, you need to add the ESP8266 board support package. Here's how to do it:

   a. Open the Arduino IDE.

   b. Go to "File" > "Preferences."

   c. In the "Additional Boards Manager URLs" field, add the following URL:
      ```
      http://arduino.esp8266.com/stable/package_esp8266com_index.json
      ```
      If there is already other text there, you may separate different URLs with a comma, e.g., `http://example.com/resouces.json, http://newexample.com/other_resource.json`
   
   d. Click "OK" to save the preferences.

   e. Go to "Tools" > "Board" > "Boards Manager."

   f. In the Boards Manager, type "ESP8266" into the search bar.

   g. Click on the "esp8266 by ESP8266 Community" entry and click the "Install" button.

   h. Wait for the installation to complete.

5. **Select the ESP8266 Board:**
   After the installation is complete, you can select the ESP8266 board you want to use. 

   a. Go to "Tools" > "Board" and select the ESP8266 board that matches your hardware (e.g., "NodeMCU 1.0 (ESP-12E Module)").

6. **Install USB Drivers (if needed):**
   Depending on your operating system, you may need to install USB drivers for the ESP8266 board. Usually, these drivers are automatically installed when you connect the board to your computer via USB. However, if you encounter driver issues, consult the documentation for your specific ESP8266 board for driver installation instructions.

7. **Select the Port:**
   Connect your ESP8266 board to your computer via USB. Then, go to "Tools" > "Port" and select the appropriate COM port or device associated with your ESP8266 board.

8. **Test with Blink Example:**
   To test if everything is set up correctly, you can upload a simple "Blink" example sketch to your ESP8266 board.

   a. Go to "File" > "Examples" > "01.Basics" > "Blink."

   b. Modify the LED pin number if necessary (the default is usually GPIO 2).

   c. Click the "Upload" button (right arrow icon) to compile and upload the sketch to your ESP8266 board.

   d. You should see the LED on your ESP8266 board blink.

That's it! You have successfully installed ESP8266 board support and dependencies on the Arduino IDE and uploaded a basic sketch to your ESP8266 board. You can now start developing and uploading your own projects to the ESP8266 board using the Arduino IDE.
