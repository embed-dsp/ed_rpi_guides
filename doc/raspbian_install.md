
# Raspbian SD Card Installation

This document describes how to install the [Raspbian](https://www.raspbian.org) 
Linux operating system on a SD Card for use with the Raspberry Pi boards.


# Download Raspbian Image

The Raspbian image can be downloaded from here: [Raspbian Download](https://www.raspberrypi.org/downloads/raspbian)

There are two version of the Raspbian image:
* Raspbian Lite
    * `2018-10-09-raspbian-stretch-lite.zip`
* Raspbian Desktop
    * `2018-10-09-raspbian-stretch.zip`

The **Lite** image is used to run the Raspberry Pi in *Headless Mode*, i.e. 
without using a physical Keybord, Mouse and Monitor.
The **Desktop** image is used to run the Raspberry Pi with full desktop environment.


# Write Raspbian Image to SD Card

## Linux

**Command Line**
* Insert SD card in the card reader
* Check mount point using the `dmesg` command
    * **NOTE:** We will here assume: `/dev/sdh`
* Unzip the *.zip image file to an *img file
    * `unzip 2018-10-09-raspbian-stretch-lite.zip`
* Write the *img file to the SD card **FIXME**: something goes wrong here, look at `dmesg`
    * `sudo dd status=progress bs=4M conv=fsync of=/dev/sdh if=2018-10-09-raspbian-stretch-lite.img`
* Unmount SD card partitions
    * `sudo umount /dev/sdh1`
    * `sudo umount /dev/sdh2`

**Fedora Media Writer**
* Install [Fedora Media Writer](https://github.com/FedoraQt/MediaWriter)
    * `sudo dnf install mediawriter`
* Insert SD card in the card reader
* Unzip the *.zip image file to an *img file
    * `unzip 2018-10-09-raspbian-stretch-lite.zip`
* Write the *img file to the SD card
    * Start `Fedora Media Writer`
    * Select: `Custom Image`
        * Open the *.img file
    * Select the SD Card and `Raspberry Pi 3 Model B`
    * Press: `Write to Disk`

## Windows

**Etcher**
* Install [Etcher](https://etcher.io)
* Insert SD card in the card reader
* Unzip the *.zip image file to an *img file
    * `unzip 2018-10-09-raspbian-stretch-lite.zip`
* Write the *img file to the SD card
    * Start `Etcher`
    * Press: `Select image`
        * Open the *.img file
    * Select the SD Card
    * Press: `Flash!`
