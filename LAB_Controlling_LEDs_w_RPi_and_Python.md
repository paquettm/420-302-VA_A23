# Lab: Controlling LEDs with Raspberry Pi and Python

This lab will teach students how to control LEDs using Python GPIO on a Raspberry Pi and display a binary count of seconds from 0 to 59.

**Objective:** In this lab, you will learn how to control LEDs using Python on a Raspberry Pi. You will write a Python program to display a binary count of seconds from 0 to 59 using LEDs.

**Materials Needed:**
- Raspberry Pi (any model with GPIO pins)
- Breadboard
- 6 LEDs
- 6 current-limiting resistors (330 ohms to 1k ohm) 
- Jumper wires

**Instructions:**

**1. Hardware Setup:**
a. Connect the Raspberry Pi to a power source and ensure it's properly configured.
b. Assemble the circuit as follows:
Refer to the pinout at https://www.raspberrypi.com/documentation/computers/raspberry-pi.html for GPIO logical pin names
- Connect the anode (longer lead) of each LED to individual GPIO pins on the Raspberry Pi (use the pins with BCM (logical) numbering 2, 3, 4, 14, 15, and 18).
- Connect the cathode (shorter lead) of each LED to a current-limiting resistor.
- Connect the other end of each resistor to the ground (GND) pin on the Raspberry Pi.

Ensure that the LEDs are connected in the correct order as per the BCM (logical) pin numbers.

**2. Python Code:**
a. Open the terminal on your Raspberry Pi.
b. Create a new Python file for your program. You can use the `nano` text editor or any other text editor of your choice:

```bash
nano binary_seconds_display.py
```

c. Copy and paste the following Python code into the `binary_seconds_display.py` file:

```python
import RPi.GPIO as GPIO # General Purpose Input/Output library
import time

# Set up the GPIO mode
GPIO.setmode(GPIO.BCM)

# Define the GPIO pins for each LED
led_pins = [2, 3, 4, 14, 15, 18]

# Initialize GPIO pins as outputs
for pin in led_pins:
    GPIO.setup(pin, GPIO.OUT)

try:
    while True: # forever until CTRL-C
        # get the current time and seconds
        current_time = time.localtime()
        seconds = current_time.tm_sec

        # convert seconds to binary string
        binary_seconds = format(seconds, '06b')

        # display each binary digit by turning LEDs on or off
        for i in range(6):
            GPIO.output(led_pins[i], int(binary_seconds[i]))

        # wait one second before resuming the program
        time.sleep(1)

finally: # when an error occurs, don't leave the try block without doing this
    # Clean up GPIO on program exit
    GPIO.cleanup()
```

Save the file and exit the text editor.

**3. Running the Program:**
a. In the terminal, run the Python program you just created:

```bash
python binary_seconds_display.py
```

Your LEDs should now start displaying a binary count of seconds from 0 to 59. Each LED represents a binary digit, and they will change to display the current seconds.

**4. Lab Questions:**
- Observe the behavior of the LEDs. What do you notice as the seconds change from 0 to 59? And 59 to 0?
- How does the `format(seconds, '06b')` function work in formatting the binary representation?
- What would you need to modify in the code if you wanted to use different GPIO pins for the LEDs?
