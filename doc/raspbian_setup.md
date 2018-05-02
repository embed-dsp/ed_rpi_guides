
# Raspbian Setup

We want to enable WiFi and the SSH service so that it is possible to work with the Raspberry Pi board in headless mode, i.e. without using a physical Keybord, Mouse and Monitor.

## Boot

* Insert SD Card into the Raspberry Pi
* Add Monitor cable to HDMI port
* Add keyboard and Mouse to USB ports
* Add LAN cable to Network (**FIXME:** Raspberry Pi 3 B/B+)
* Turn on power

**FIXME:** (Raspberry Pi 3 B/B+)
Note the IP address for the LAN shown as: `My IP address is xxx.xxx.xxx.xxx`

## Console Login
* Login: `pi`
* Password: `raspberry`

## Enable SSH service

Enable SSH:
```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P2 SSH**

```bash
logout
```

We can now perform remote login using SSH **FIXME:** and the HDMI cable to the monitor, the Keyboard and the Mouse can be removed.
FIXME: Keep the LAN cable connected until we have enabled WiFi

## SSH Login

* Login: `ssh pi@xxxx.xxxx.xxx.xxx`
* Password: `raspberry`

## Enable Wireless Network (WiFi) on Raspberry Pi 3 B+
FIXME: In Denmark the "Localisation Options" must be set before the wlan0 interface shows up!

```bash
sudo raspi-config
```

* Select: **4 Localisation Options**
    * Select: **I4 Change Wi-fi Country**

* Select: **2 Network Options**
    * Select: **N2 Wi-fi**

## Enable Wireless Network (WiFi)

List the available WiFi networks:
```bash
sudo iwlist wlan0 scan | grep ESSID
```

Enter directory with network configuration file:
```bash
cd /etc/wpa_supplicant
```

Edit configuration file:
```bash
sudo vi wpa_supplicant.conf
```

Enter the following text in the configuration file:
```bash
country=DK
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="FIXME: Type your SSID here"
    psk="FIXME: Type your password here"
}
```

Force a re-read of updated configuration file and start `wlan0` network:
```bash
sudo wpa_cli -i wlan0 reconfigure
```

Get the assigned WiFi IP address by looking at the `wlan0` network interface:
```bash
ifconfig
```

## Enable HW Interfaces

Enable **SPI** interface:
```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P4 SPI**

Enable **I2C** interface:
```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P5 I2C**

Enable **UART** interface:
```bash
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P6 Serial**
        * Select: **No login shell**
        * Select: **Enable serial port hardware**

**FIXME:** Advanced Options / Audio (Auto)

## Change Keyboard Layout

Enter directory with keyboard configuration file:
```bash
cd /etc/default
```

Edit configuration file:
```bash
sudo vi keyboard
```

Switch to US keyboard:
```bash
XKBLAYOUT="us"
```

Retart keyboard service.
```bash
sudo service keyboard-setup restart
```

**FIXME:** Reboot to activate the new keyboard layout:
```bash
reboot
```

**FIXME:** login again

## Update packages
FIXME:
```bash
sudo apt-get update
```

FIXME:
```bash
sudo apt-get upgrade
```

## Install new packages
```bash
sudo apt-get install vim
sudo apt-get install emacs
sudo apt-get install tree
sudo apt-get install git
sudo apt-get install sox
```

## Enable Syntax Highlighting for VIM
```bash
cd /home/pi
vim .vimrc
--------------------
syntax on
```

## Enable more Bash aliases
```bash
cd /home/pi
vim .bashrc
--------------------
alias ll='ls -l'
alias la='ls -A'
```

## Install **ed_rpi** package
FIXME:
```bash
cd /home/pi
git clone https://github.com/embed-dsp/ed_pi.git
cd ed_pi
vim Makefile
...
make build
sudo make install
```

FIXME:
```bash
cd /etc
sudo vim rc.local

# Run at constant maximum clock frequency.
/opt/ed_pi/bin/cpu_set_performance.sh
```
