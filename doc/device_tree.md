
# Device Tree

This document describes the basic usage of Device Trees in the Raspberry Pi.


# File Extensions

Extension | Description
----------|--------------------------
*.dts     | Device Tree source
*.dtb     | Device Tree blob
*.dtbo    | Device Tree blob overlay


# Command Line Tools

Tool       | Description
-----------|-------------------------
dtc        | Device Tree compiler
dtoverlay  | Device Tree overlay tool


# Save the current live Device Tree to file

The live Device Tree is located here in the file system on the Raspberry Pi:

```bash
/proc/device-tree
```

Save as blob in file `foo.dtb`
```bash
dtc -I fs -O dtb -o foo.dtb /proc/device-tree
```

Save as source in file `foo.dts`
```bash
dtc -I fs -O dts -o foo.dts /proc/device-tree
```


# Compile Device Tree source to Device Tree blob overlay

Compile source file `foo.dts` to blob overlay file `foo.dtbo`
```bash
dtc -I dts -O dtb -o foo.dtbo foo.dts
```


# Load / Unload Device Tree blob overlay

Load Device Tree blob overlay `foo.dtbo` from default location `/boot/overlays`
```bash
dtoverlay foo
```

Load Device Tree blob overlay `foo.dtbo` from alternative location `/hello/world`
```bash
dtoverlay -d /hello/world foo
```

Unload Device Tree blob overlay
```bash
dtoverlay -r foo
```


# List loaded Device Tree blob overlays
```bash
dtoverlay -l
```
