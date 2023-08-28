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

## Validating the Configuration

Once your SD card has been written and verified by Raspberry Pi Imager, you may eject it from the PC and insert it into the unpowered Raspberry Pi device.

### Network Connection

Connect the Raspberry Pi device (RPi) to a compatible power supply and allow a few minutes for it to boot up.

If the RPi and the wireless network have been configured correctly, then it should be possible to find the device on the local network, by adding `.local` to the end of the hostname.
Frist try pnging the RPi, using its hostname, for example:

```
ping hostname.local
```

If the device is found, try connecting to it using `ssh` with your user name and hostname as follows:

```
ssh user@hostname.local
```

If the device is found, accept the key and enter the password.

### Gadget Mode Connection

If network connections fail or a local WiFi network is not available, you may fallback on gadget mode.

Follow the set up procedure outlined at [https://github.com/paquettm/raspberry-pi-OS-setup/blob/main/gadget_mode/README.md](https://github.com/paquettm/raspberry-pi-OS-setup/blob/main/gadget_mode/README.md)

To use gadget mode, you must connect the RPi to the computer as a device using a USB cable (data and power leads need to be functional) connected to the RPi power port.
Allow a few minutes for it to boot up.

If the connection via gadget mode is successful, then the above checks will provide positive results.

### VNC Setup

If the Network Connection or the Gadget Mode Connection with the RPi has been successful, and you have connected to it via SSH, then you have access to the RPi command prompt.

To set up VNC, type

```
sudo raspi-config
```

Enter your user account password if required.

Navigate to **Interface Options** and then **VNC** and select **Yes**.

Exit the raspi-config program.

In the unlikely case you must reboot, type 
```
sudo reboot
```

### VNC Connection

To complete a VNC connection, you need to have a VNC client installed on your computer or a portable VNC client application.
You may download a portable VNC client from [https://www.realvnc.com/en/connect/download/viewer/](https://www.realvnc.com/en/connect/download/viewer/).

With the RPi connected as previously functional, connect your VNC client to `hostname.local`, accept any fingerprint or key and then enter your account information.

You should now have access to the graphical desktop.

## Explore

Get a feel for the environment and try to understand why your RPi is not connected onto the wireless network.
Try using raspi-config to connect your RPi to the wireless network.

