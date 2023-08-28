# SD Card Preparation

To be able to boot up your Raspberry Pi, you must have an Operating System with a working configuration installed on its boot medium.

By default, Raspberry Pi devices will boot up from a micro SD card inserted in a port for this purpose on the backside of the SBC.
Some models can also be made to boot up from USB, which can be more practical.

## Imaging Software

To write an image onto an SD card, your host computer needs software with disk imaging capabilities.
For operating systems specific to Raspberry Pi devices, the most practical software of this kind is **Raspberry Pi Imager**.

If this software is already installed on your workstation, and the apropriate permissions are set for it or for your user account, then you can proceed.
Otherwise, you will need to install the software, which will require appropriate software installation permissions on your user account.

Navigate to [https://www.raspberrypi.com/software/](https://www.raspberrypi.com/software/).
Click on the link matching your operating system to start the download.
Navigate in your operating system to the location of this download and execute the installer file.
Follow the steps to complete installation.

## Creating the New SD Card

Start the Raspberry Pi Imager software.

### OS Choice
Click on **CHOOSE OS**.
You can select **Rasperry Pi OS (32-bit)** for any RPi unit or **Raspberry Pi OS (other)** and **Rasperry Pi OS (64-bit)** if oyu have a RPi 3, 4, or 400.
Next, click on the gear icon that appeared at the lower right to set up installation options.

### Hostname
Check the **Set hostname:** box and write a unique name for that hostname: your last name followed by "-pi", e.g., I would call mine **paquette-pi**.
This is important to ease the network connection process, since conflicting names will cause issues down the line.

### SSH

SSH is a way to securly connect to devices over networks.

Check the **Enable SSH** box and ensure that the **Use password authentication** radio button is selected.

### Username and Password

Ensure that the **Set username and password** box is checked and enter your first name as the username and a password which you will not forget.

### Configure Wireless LAN

We will set up a temporary network to connect to the Raspberry Pi devices.

Check the **Configure wireless LAN** box and write the SSID and password information provided for this network.
Note that Enterprise Wireless LANs are harder to join and the option to do so is not included in the Raspberry Pi Imager as far as this author knows.

### Locale Settings

Check the **Set locale settings** box to inform the RPi of the timezone and keyboard settings.
These settings should be **America/Toronto** and **us**, respectively.
Click **Save**.

### Storage

Connect your SD card to the host computer.
You may need a USB interface for this or your computer may have a dedicated SD card connector that may or may not require a size adapter.
Click **CHOOSE STORAGE**.
In the list, select the SD card that you connected to the host computer.
Do not select another disk because the next operation will be fatal to any data stored on the disk that will be imaged.

One way to ensure that you have selected the correct drive is to open the selection menu without th SD card connected to the system and then connect the SD card to the system, seleting this new device.

### Writing the Image

Click on **WRITE**.
Heed the warnings.
Proceed at your own risk.
