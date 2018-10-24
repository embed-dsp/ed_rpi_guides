
# Raspbian Setup

This document describes how perform basic setup of Raspbian from a newly installed SD card.


# Boot

* Insert SD Card into the Raspberry Pi
* Add Monitor cable to HDMI port
* Add Keyboard to USB port
* Turn on Power

For Raspberry Pi 3 B/B+ you can also
* Add Mouse to USB port
* Add LAN cable to Network

**NOTE**: When Raspberry Pi 3 B/B+ has booted with LAN cable connected to the network
then one of the last lines on the console output will display: `My IP address is xxx.xxx.xxx.xxx`


# Console Login

Perform a console login to the Raspberry by typing the following:

* Login: `pi`
* Password: `raspberry`


# Enable SSH service

We want to enable the SSH service so that it is possible to work with the Raspberry Pi board in
*Headless Mode*, i.e. without using a physical Keybord, Mouse and Monitor.

```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P2 SSH**


# Enable Wireless Network (WiFi)

Enable WiFi to enable remote SSH login to the Raspberry.

```bash
sudo raspi-config
```

* Select: **4 Localisation Options**
    * Select: **I4 Change Wi-fi Country**

* Select: **2 Network Options**
    * Select: **N2 Wi-fi**

**NOTE**: On Raspberry Pi 3 B+ the *Wi-fi Country* must be set correctly before the wlan0 interface shows up!

**NOTE**: The Raspberry Pi Zero W does NOT support WiFi in the 5GHz band

The WiFi settings are stored in the file:
```bash
/etc/wpa_supplicant/wpa_supplicant.conf
```

The contents of this file looks like this:
```bash
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=DK      # NOTE: This is set by: I4 Change Wi-fi Country 

network={
	ssid="..."
	psk="..."
}
```

The WiFi settings can also be changed by manually editing the `wpa_supplicant.conf` file:
```bash
sudo vi /etc/wpa_supplicant/wpa_supplicant.conf
```

## Command Line Utilities

Force a re-read of the `wpa_supplicant.conf` file and start `wlan0` network:
```bash
sudo wpa_cli -i wlan0 reconfigure
```

List all of the configured WiFi networks:
```bash
sudo wpa_cli -i wlan0 list_networks
```

List all of the available WiFi networks:
```bash
sudo iwlist wlan0 scan | grep ESSID
```

Get the assigned WiFi IP address by looking at the `wlan0` network interface:
```bash
ifconfig wlan0
```


# Remote SSH Login

Now that the WiFi has been setup we are able perform a remote SSH login to the Raspberry to finish the setup.

* Login: `ssh pi@xxxx.xxxx.xxx.xxx`
* Password: `raspberry`


# Change Keyboard Layout

Change the default keyboard layout from GB (Great Britain) to what matches your needs:

```bash
sudo raspi-config
```

* Select: **4 Localisation Options**
    * Select: **I3 Change Keyboard Layout**

The keyboard settings are stored in the file:
```bash
/etc/default/keyboard
```

The contents of this file looks like this:
```bash
# KEYBOARD CONFIGURATION FILE

# Consult the keyboard(5) manual page.

XKBMODEL="pc105"
XKBLAYOUT="us"
XKBVARIANT=""
XKBOPTIONS=""

BACKSPACE="guess"
```

The keyboard layout can also be changed by manually editing the `keyboard` file:
```bash
sudo vi /etc/default/keyboard
```


# Change Timezone

Change the default timezone to what matches your needs:

```bash
sudo raspi-config
```

* Select: **4 Localisation Options**
    * Select: **I2 Timezone**

The timezone settings are stored in the files:
```bash
# File
/etc/timezone

# Link
/etc/localtime -> /usr/share/zoneinfo/Europe/Copenhagen
```


# apt Command Guide
Here is a summary of some usefull `apt` commands.
```bash
# List all available packages.
sudo apt-cache pkgnames

# Search for a specific package.
sudo apt-cache search <package-name>

# Get information about a specific package.
sudo apt-cache show <package-name>

# Get information about a dependencies of a specific package.
sudo apt-cache showpkg <package-name>

# Resynchronize the package index files.
sudo apt-get update

# Install the newest versions of all packages.
sudo apt-get upgrade

# Install specific package.
sudo apt-get install <package-name>
```


# Install extra Packages

Install some extra packages that are useful while working on the Raspberry Pi:
```bash
# Version control.
sudo apt-get install git
```

```bash
# File system utilities.
sudo apt-get install tree
sudo apt-get install dos2unix
```

```bash
# Text editors.
sudo apt-get install vim
sudo apt-get install emacs
```

```bash
# Audio utilities.
sudo apt-get install sox
sudo apt-get install flac
sudo apt-get install madplay
```

# Enable Syntax Highlighting for VIM

Edit the `.vimrc` file:
```bash
vim /home/pi/.vimrc
```

and type following:
```bash
syntax on
```


# Enable more Bash aliases

Edit the `.bashrc` file:
```bash
vim /home/pi/.bashrc

```

and enable the following aliases (around line 90 in the `.bashrc` file)
```bash
alias ll='ls -l'
alias la='ls -A'
```


# Enable Hardware Interfaces

The following hardware interfaces can be accessed from *User Space* 
after they have been enabled.

## SPI

Enable SPI interface:
* `/dev/spidev0.0`
* `/dev/spidev0.1`

```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P4 SPI**

## I2C

Enable I2C interface:
* `/dev/i2c-1`

```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P5 I2C**

## UART

Enable UART interface:
* `/dev/ttyS0`
* `/dev/serial0 -> /dev/ttyS0`

```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P6 Serial**
        * Select: **No login shell**
        * Select: **Enable serial port hardware**
