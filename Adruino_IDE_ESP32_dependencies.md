# Arduino IDE & ESP32
To install ESP32 dependencies on the Arduino IDE, follow these steps:

1. **Install the Arduino IDE:**
   If you haven't already, download and install the Arduino IDE from the official website (https://www.arduino.cc/en/software).

2. **Open Arduino IDE:**
   Launch the Arduino IDE on your computer.

3. **Add ESP32 Board Support:**
   To program ESP32 boards with the Arduino IDE, you need to add the ESP32 board support package. Here's how to do it:

   a. Open the Arduino IDE.

   b. Go to "File" > "Preferences."

   c. In the "Additional Boards Manager URLs" field, add the following URL:
      ```
      https://dl.espressif.com/dl/package_esp32_index.json
      ```
      If there is already other text there, you may separate different URLs with a comma, e.g., `http://example.com/resouces.json, http://newexample.com/other_resource.json`

   d. Click "OK" to save the preferences.

   e. Go to "Tools" > "Board" > "Boards Manager."

   f. In the Boards Manager, type "ESP32" into the search bar.

   g. Click on the "ESP32 by Espressif Systems" entry and click the "Install" button.

   h. Wait for the installation to complete.

4. **Select the ESP32 Board:**
   After the installation is complete, you can select the ESP32 board you want to use. 

   a. Go to "Tools" > "Board" and select the ESP32 board you have (e.g., "ESP32 Dev Module").

5. **Install USB Drivers (if needed):**
   Depending on your operating system, you may need to install USB drivers for the ESP32 board. Usually, these drivers are automatically installed when you connect the board to your computer via USB. However, if you encounter driver issues, consult the documentation for your specific ESP32 board for driver installation instructions.

6. **Select the Port:**
   Connect your ESP32 board to your computer via USB. Then, go to "Tools" > "Port" and select the appropriate COM port or device associated with your ESP32 board.

7. **Test with Blink Example:**
   To test if everything is set up correctly, you can upload a simple "Blink" example sketch to your ESP32 board.

   a. Go to "File" > "Examples" > "01.Basics" > "Blink."

   b. Modify the LED pin number if necessary (the default is usually pin 2).

   c. Click the "Upload" button (right arrow icon) to compile and upload the sketch to your ESP32 board.

   d. You should see the LED on your ESP32 board blink.

That's it! You have successfully installed the ESP32 board support and dependencies on the Arduino IDE and uploaded a basic sketch to your ESP32 board. You can now start developing and uploading your own projects to the ESP32 board using the Arduino IDE.
