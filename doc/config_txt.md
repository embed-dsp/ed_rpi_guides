
# config.txt

This document describes how the Raspberry Pi can be configured with the 
`/boot/config.txt` file.


# Enable / Disable On-Board Audio

```bash
# Enable
dtparam=audio=on

# Disable
dtparam=audio=off
```

## Modules
* `snd_bcm2835`
* `snd_pcm`
* `snd_timer`
* `snd`


# Enable / Disable primary Console UART

```bash
# Enable
enable_uart=1

# Disable
enable_uart=0
```

## Modules
* `serdev`

## User Space Devices
* `/dev/serial0`
* `/dev/ttyS0`


# Enable / Disable SPI

```bash
# Enable
dtparam=spi=on

# Disable
dtparam=spi=off
```

## Modules
* `spi_bcm2835`
* `spidev`

## User Space Devices
* `/dev/spidev0.0`
    * This device controls CE0# on the SPI0 device.
* `/dev/spidev0.1`
    * This device controls CE1# on the SPI0 device.


# Enable / Disable I2C

```bash
# Enable
dtparam=i2c_arm=on

# Disable
dtparam=i2c_arm=off
```

## Modules
* `i2c_bcm2835`
* `i2c_dev`

## User Space Devices
* `/dev/i2c-1`
