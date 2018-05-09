
# C/C++ Cross Compile Toolchains

This document describes some of the cross compler toolchains that can be used with Raspberry Pi.


# Toolchain Naming Conventions

Toolchains typically have a loose naming convention like: `arch[-vendor][-os]-abi`.

Name   | Description
-------|----------------------------------------------------------------------------------------
arch   | Architecture: `arm`, `mips`, `x86`, `i686`, ...
vendor | Tool chain supplier: `apple`, ...
os     | Operating system: `linux`, `none` (Bare Metal)
abi    | Application-Binary-Interface (ABI) convention: `eabi`, `eabihf`, `gnueabi`, `gnueabihf`

Application-Binary-Interface (ABI) conventions:

Name      | Tagret Operating System                                      | Default Floating Point Options
----------|--------------------------------------------------------------|-------------------------------------------
gnueabi   | Linux (using [glibc](https://www.gnu.org/software/libc))     | `-mfloat-abi=soft` or `-mfloat-abi=softfp`
gnueabihf | Linux (using [glibc](https://www.gnu.org/software/libc))     | `-mfloat-abi=hard`
eabi      | Bare Metal (using [newlib](https://sourceware.org/newlib) ?) | `-mfloat-abi=soft` or `-mfloat-abi=softfp`
eabihf    | Bare Metal (using [newlib](https://sourceware.org/newlib) ?) | `-mfloat-abi=hard`


# Raspberry Pi Cross Compiler Toolchain

FIXME: Elaborate ... [GitHub Repository](https://github.com/raspberrypi/tools)

## gcc-4.9.3

Toolchain                     | Host             | Default Target Options
------------------------------|------------------|------------------------------------------------------------------------------------------------
arm-rpi-4.9.3-linux-gnueabihf | Linux x86 64-bit | `-mlittle-endian`, `-march=armv6` (32-bit), `-mtune=[default]`, `-mfloat-abi=hard`, `-mfpu=vfp`

## gcc-4.8.3

Toolchain                                   | Host             | Default Target Options
--------------------------------------------|------------------|--------------------------------------------------------------------------------------------------
gcc-linaro-arm-linux-gnueabihf-raspbian     | Linux x86 32-bit | `-mlittle-endian`, `-march=armv6` (32-bit), `-mtune=arm1176jz-s`, `-mfloat-abi=hard`, `-mfpu=vfp`
gcc-linaro-arm-linux-gnueabihf-raspbian-x64 | Linux x86 64-bit | `-mlittle-endian`, `-march=armv6` (32-bit), `-mtune=arm1176jz-s`, `-mfloat-abi=hard`, `-mfpu=vfp`

## gcc-4.7.1

Toolchain                       | Host             | Default Target Options
--------------------------------|------------------|----------------------------------------------------------------------------------------------------
arm-bcm2708-linux-gnueabi       | Linux x86 32-bit | `-mlittle-endian`, `-march=armv2` (32-bit), `-mtune=arm1176jz-s`, `-mfloat-abi=softfp`, `-mfpu=fpa`
arm-bcm2708hardfp-linux-gnueabi | Linux x86 32-bit | `-mlittle-endian`, `-march=armv2` (32-bit), `-mtune=arm1176jz-s`, `-mfloat-abi=hard`, `-mfpu=fpa`

## Installation

```bash
# Create installation folder.
mkdir -p /opt/raspberry

# Enter installation folder.
cd /opt/raspberry

# Clone repository.
git clone https://github.com/raspberrypi/tools.git
```


# Linaro Cross Compiler Toolchain

FIXME: Elaborate ... [Downloads](https://www.linaro.org/downloads)

## Tagret Operating System: Linux (Using [glibc](https://www.gnu.org/software/libc))

Toolchain                                              | Host             | Default Target Options
-------------------------------------------------------|------------------|-----------------------------------------------------------------------------------------------------------------------
gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabihf    | Linux x86 64-bit | `-mlittle-endian`, `-march=armv7-a` (32-bit), `-mtune=cortex-a9`, `-mthumb`, `-mfloat-abi=hard`, `-mfpu=vfpv3-d16`
gcc-linaro-7.2.1-2017.11-x86_64_armv8l-linux-gnueabihf | Linux x86 64-bit | `-mlittle-endian`, `-march=armv8-a` (32-bit), `-mtune=[default]`, `-mthumb`, `-mfloat-abi=hard`, `-mfpu=neon-fp-armv8`
gcc-linaro-7.2.1-2017.11-x86_64_aarch64-linux-gnu      | Linux x86 64-bit | `-mlittle-endian`, `-march=armv8-a` (64-bit), ...

## Tagret Operating System: Bare Metal (Using [newlib](https://sourceware.org/newlib) ?)

Toolchain                                   | Host             | Default Target Options
--------------------------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------
gcc-linaro-7.2.1-2017.11-x86_64_arm-eabi    | Linux x86 64-bit | `-mlittle-endian`, `-march=armv2` (32-bit), `-mtune=[default]`, `-marm`, `-mthumb-interwork`, `-mfloat-abi=soft`, `-mfpu=vfp`
gcc-linaro-7.2.1-2017.11-x86_64_aarch64-elf | Linux x86 64-bit | `-mlittle-endian`, `-march=armv8-a` (64-bit)

## Installation

```bash
# Create installation folder.
mkdir -p /opt/linaro

# Enter installation folder.
cd /opt/linaro

# Download.
wget https://releases.linaro.org/components/toolchain/binaries/latest/arm-linux-gnueabihf/gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabihf.tar.xz

# Extract.
tar xf gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabihf.tar.xz
```


# Misc

Information about gcc executable (32/64-bit etc.)
```bash
file gcc
```

Overview of gcc command line options
```bash
gcc --help
```

Information about gcc version
```bash
gcc --version
```

Information about gcc target options
```bash
gcc -Q --help=target
```

Information about gcc optimization options
```bash
gcc -Q --help=optimizers
```
