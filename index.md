---
title: Home
layout: home
nav_order: 1
---


# Klipper USB Flashing Guide

So you want to install Klipper onto your 3D printer. Wonderful! While the process may seem a little daunting the first time it really isn't that complicated and this guide will step you through each part in simple steps.

Before we get started, a little background information.

Klipper on a 3D printer comprises of two parts, the Klipper Service side running on a computer (usually a Raspberry Pi, but any computer almost any computer can work) and then the Klipper *firmware* that is flashed to the actual 3D printer board inside your printer.

This guide is how to flash the *firmware* part of the process, so it assumes you already have some sort of computer running that has the Klipper service/software side installed and functioning.

Please note that whenever you see "Pi" or "RPi" in this guide you should substitute it for whatever computer you are running Klipper on (Raspberry Pi, Orange Pi, CB1, BTT Pi, old laptop etc). For example, if the guide says "plug the USB into the Pi", and you have an old laptop doing this job, then plug the USB into your old laptop.
Also note that integrated boards like the BTT Manta series that have a CM4/CB1/CB2 module *on* the mainboard itself, then any Pi connections (usb, etc) would actuallly be on the Manta/Mainboard, and not the Pi/Computer board.

# Why Katapult?

Katapult is a small bit of bootloader firmware *seperate* to Klipper. You can technically install Klipper firmware perfectly fine without ever touching katapult, and you will find that (almost) every other guide or manufacturer user manual chooses this non-katapult method.

I prefer to use Katapult instead and overwriting the "stock" board bootloader in the process. The stock bootloader on a lot of boards is the little bit of code that lets you flash the board firmware via a micro-SD card, and they almost universally suck. Replacing this stock bootloader with Katapult lets you simply flash/update your Klipper firmware over a USB connection with no physical interaction required with the board being flashed (no more flipping a printer and removing panels).

# My board isn't listed

If the particular board you want to flash isn't already in the [Hardware Config List](./hardware_config/hardware_config.md), or if the entry has incorrect information, please lodge a [Pull Request](https://github.com/Esoterical/klipper_usb_flashing/pulls) or raise an [Issue](https://github.com/Esoterical/klipper_usb_flashing/issues)

# Let's Go!

If this is the first time you are flashing Klipper to your board, or at least the first time doing it using *this* guide, then please:

[Click Here if your board uses an STM32 MCU chip](./initial_stm32.md)

[Click Here if your board uses an RP2040 MCU chip](./initial_rp2040.md)

If your board already has both Katapult and Klipper flashed to it (either after using this guide or it came from the manufacturer this way) and you just need to update Klipper to a new version, [Click Here for the Updating page](./updating.md)
