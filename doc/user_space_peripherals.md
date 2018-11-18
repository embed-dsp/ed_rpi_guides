
# User Space Peripherals

The following hardware interfaces can be accessed from *User Space* 
after they have been enabled.

This document describes how the Raspberry Pi can be configured with the 
`/boot/config.txt` file.


# On-Board Audio

```sh
# Enable
dtparam=audio=on
```

```sh
# Disable
dtparam=audio=off
```

## Modules
* `snd_bcm2835`
* `snd_pcm`
* `snd_timer`
* `snd`


# Primary Console UART

```sh
# Enable
enable_uart=1
```

```sh
# Disable
enable_uart=0
```

```sh
sudo raspi-config
```
* Select: **5 Interfacing Options**
    * Select: **P6 Serial**
        * Select: **No login shell**
        * Select: **Enable serial port hardware**

## Modules
* `serdev`

## User Space Devices
* `/dev/serial0`
* `/dev/serial0 -> /dev/ttyS0`


# SPI0

```sh
# Enable
dtparam=spi=on
```

```sh
# Disable
dtparam=spi=off
```

## Modules
* `spi_bcm2835`
* `spidev`

## User Space Devices
* `/dev/spidev0.0`
    * This device controls `CE0_N` on the SPI0 device.
* `/dev/spidev0.1`
    * This device controls `CE1_N` on the SPI0 device.


# SPI1

```sh
# Enable ...
dtoverlay=spi1-1cs
```

```sh
# Enable ...
dtoverlay=spi1-2cs
```

```sh
# Enable ...
dtoverlay=spi1-3cs
```

## Modules
* `spi_bcm2835aux`
* `spidev`

## User Space Devices
* `/dev/spidev1.0`
    * This device controls `CE0_N` on the SPI1 device.
* `/dev/spidev1.1`
    * This device controls `CE1_N` on the SPI1 device.
* `/dev/spidev1.2`
    * This device controls `CE2_N` on the SPI1 device.


# I2C0

```sh
# Enable
dtparam=i2c_vc=on
```

```sh
# Disable
dtparam=i2c_vc=off
```

## Modules
* `i2c_bcm2835`
* `i2c_dev`

## User Space Devices
* `/dev/i2c-0`


# I2C1

```sh
# Enable
dtparam=i2c_arm=on
```

```sh
# Disable
dtparam=i2c_arm=off
```

```sh
# FIXME: ...
dtparam=i2c_arm_baudrate=400000
```

## Modules
* `i2c_bcm2835`
* `i2c_dev`

## User Space Devices
* `/dev/i2c-1`
