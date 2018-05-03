
# Pimoroni pHAt DAC

This document describes how to install the 
[Pimoroni pHAt DAC](https://shop.pimoroni.com/products/phat-dac) board on Raspberry Pi.


# Install

Edit the file `/boot/config.txt`
```bash
sudo vim /boot/config.txt
```

Disable on-board audio
```bash
# dtparam=audio=on
```

Enable I2S audio output (loads `snd_soc_hifiberry_dac` module)
```bash
dtoverlay=hifiberry-dac
```

Reboot Raspberry Pi
```bash
sudo reboot
```


# Check

Check if ALSA has detected the sound card for playback.
```bash
aplay -l
```

The resulting output should look like this
```
**** List of PLAYBACK Hardware Devices ****
card 0: sndrpihifiberry [snd_rpi_hifiberry_dac], device 0: HifiBerry DAC HiFi pcm5102a-hifi-0 []
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```
