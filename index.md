---
title: Home
layout: home
nav_order: 1
---


# Klipper USB Flashing Guide

So you want to install Klipper onto your 3D printer. Wonderful! While the process may seem a little daunting the first time it really isn't that complicated and this guide will step you through each part in simple steps.

Before we get started, a little background information.

Klipper on a 3D printer comprises of two parts, the Klipper Service side running on a computer (usually a Raspberry Pi, but almost any computer can work) and then the Klipper *firmware* that is flashed to the actual 3D printer board inside your printer.

This guide is how to flash the *firmware* part of the process, so it assumes you already have some sort of computer running that has the Klipper service/software side installed and functioning.

Please note that whenever you see "Pi" or "RPi" in this guide you should substitute it for whatever computer you are running Klipper on (Raspberry Pi, Orange Pi, CB1, BTT Pi, old laptop etc). For example, if the guide says "plug the USB into the Pi", and you have an old laptop doing this job, then plug the USB into your old laptop.
Also note that integrated boards like the BTT Manta series that have a CM4/CB1/CB2 module *on* the mainboard itself, then any Pi connections (usb, etc) would actuallly be on the Manta/Mainboard, and not the Pi/Computer board.

# Why Katapult?

Katapult is a small bit of bootloader firmware *seperate* to Klipper. You can technically install Klipper firmware perfectly fine without ever touching katapult, and you will find that (almost) every other guide or manufacturer user manual chooses this non-katapult method.

I prefer to use Katapult instead and overwriting the "stock" board bootloader in the process. The stock bootloader on a lot of boards is the little bit of code that lets you flash the board firmware via a micro-SD card, and they almost universally suck. Replacing this stock bootloader with Katapult lets you simply flash/update your Klipper firmware over a USB connection with no physical interaction required with the board being flashed (no more flipping a printer and removing panels).

# Toolhead Cabling

If you are using a USB toolhead (Nitehawk, SB2209-USB, SB Combo V2, etc.) it is *extremely* important to have the main cable properly supported
and strain relieved. A cable that has constant sharp bends during motion or a toolhead board connector that is wiggling around will soon develop
communication issues.

A common method of supporting and strain relieving the umbilcal is to use PG7 glands, and although these work really well they also tend to mean people have to cut or repin the premade cables that come with some boards. Because of this I prefer using the printable [P.U.G](https://www.printables.com/model/378567-pug-parametric-umbilical-gland) umbilical gland. It does the same job as a PG7 but comes in two halves so you can clamp it over any cable without needing to cut/depin anything.

I've got a public Printables "collection" of various PUG mounts for different extruders [here](https://www.printables.com/@Esoterical_306854/collections/2039742) and will hopefully grow it over time, so be sure to check there to see if one of them fits your toolboard/extruder.

Note, this is only really relevant for Toolhead boards that are moving around the printer. For boards that don't move (like a mainboard or a
board running a multi-material device of some kind) standard USB cables would be fine (as long as they can't get bumped loose).

# Let's Go!

If this is the first time you are flashing Klipper to your board, or at least the first time doing it using *this* guide, then please:

[Click Here if your board uses an STM32 MCU chip](./initial_stm32.md)

[Click Here if your board uses an RP2040 MCU chip](./initial_rp2040.md)

If your board already has both Katapult and Klipper flashed to it (either after using this guide or it came from the manufacturer this way) and you just need to update Klipper to a new version, [Click Here for the Updating page](./updating.md)
