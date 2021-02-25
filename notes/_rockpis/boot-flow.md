---
title: "Boot flow"
layout: note
updated: "2021-02-25"
---

Basic ROCK Pi S boot flow involves two stages. However, to load a fully-functional operating system requires more.

## Stage 1 -- Primary Program Loader

The Primary Program Loader (PPL) resides **_in internal 32K BootROM_** inside SoC. Its purpose is to prepare the device for the second-stage boot loader.

Upon reset, CPU starts executing BootROM code at address `0xffff0000`. BootROM code performs minimal system initialization, then searches for a Secondary Program Loader (SPL) on external boot devices, loads SPL into internal 256K SRAM, and gives it control.

While searching for SPL, BootROM code probes external devices for ID Block, a 512-bytes structure containing information about the size of SPL, its location on bootable medium, and other data.

Boot devices are probed for ID Block in order:<br>
NAND Flash > eMMC > SPI NOR Flash > SPI NAND Flash > SDMMC.

**_ROCK Pi S supports booting from microSD card or on-board SD NAND flash memory_** (if present). If boot code is not ready in these devices, USB OTG is initialized to allow boot code upload.

## Stage 2 -- Secondary Program Loader

SPL is **_loaded from an external boot device and runs in internal on-chip SRAM_**. Its purpose is to initialize the main system memory (external DRAM) and load a target application that can be either a full-fledged operating system loader or a standalone bare-metal application.

The most common options to use as the second-stage boot loader for ROCK Pi S are _Rockchip Loader_, a proprietary software, and _U-Boot_, which is open-source.

### Rockchip Loader

Rockchip Loader for SD comprises three modules, all required:

- `ddrbin` - configures DRAM and UART
- `miniloader` - application loader
- `bl31` - Trusted Firmware-A (TF-A) image for AArch64

These modules run in sequence and perform the following actions:

- `ddrbin` initializes DRAM and configures **_UART (1.5 Mbps, 8 data bits, 1 stop bit, no parity, no flow control)_**;
- `miniloader` loads TF-A executable and target application into DRAM;
- `miniloader` gives control to TF-A in secure state (EL3);
- TF-A performs its part of initialization, then transfers control to the target application in non-secure state (EL2).

Pre-compiled Rockchip Loader binaries can be found on [GitHub](https://github.com/radxa/rkbin){:target="_blank"}.

### U-Boot

U-Boot is a powerful open-source boot loader for embedded devices. It supports a variety of architectures and can be configured as both a first-stage and second-stage boot loader.

For information, see [Wikipedia](https://en.wikipedia.org/wiki/Das_U-Boot){:target="_blank"} and the official GitHub [repository](https://github.com/u-boot/u-boot){:target="_blank"}.

_Details about using U-Boot with ROCK Pi S are **~~_out of scope_~~** for now._
