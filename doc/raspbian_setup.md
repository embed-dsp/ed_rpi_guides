
# Raspbian Setup

This document describes how perform basic setup of Raspbian from a newly installed SD card.


# Boot

* Insert SD Card into the Raspberry Pi
* Add Monitor cable to HDMI port
* Add keyboard and Mouse to USB ports (**FIXME:** Raspberry Pi 3 B/B+)
* Add LAN cable to Network (**FIXME:** Raspberry Pi 3 B/B+)
* Turn on power

**FIXME:** (Raspberry Pi 3 B/B+)
When Raspberry Pi has booted one of the last lines on the console output
will display: `My IP address is xxx.xxx.xxx.xxx`
Take note of this IP address since we will use it to perform remote SSH login to complete the setup process.


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

We can now perform remote login using SSH and the HDMI cable to the monitor, the Keyboard and the Mouse can be removed.
**NOTE**: Keep the LAN cable connected until we have enabled WiFi.


# Remote SSH Login

Perform a remote SSH login to the Raspberry to finish the setup.

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


# Enable Wireless Network (WiFi)

Enable WiFi to enable remote SSH login to the Raspberry without using a LAN cable.

```bash
sudo raspi-config
```

* Select: **4 Localisation Options**
    * Select: **I4 Change Wi-fi Country**

* Select: **2 Network Options**
    * Select: **N2 Wi-fi**

**NOTE**: On Raspberry Pi 3B+ the *Wi-fi Country* must be set before the wlan0 interface shows up!

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


# Update Packages

Type the following commands to update all of the packages to the latest versions:
```bash
# Resynchronize the package index files
sudo apt-get update

# Install the newest versions of all packages
sudo apt-get upgrade
```


# Install extra Packages

Install some extra packages that are useful while working on the Raspberry Pi:
```bash
sudo apt-get install git
sudo apt-get install tree
sudo apt-get install vim
sudo apt-get install emacs
sudo apt-get install sox
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
