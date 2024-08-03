---
layout: default 
title: Updating
has_children: false
nav_order: 40
has_toc: false
---

# Updating

![captain_update](https://github.com/Esoterical/voron_canbus/assets/124253477/2b35e7a5-d2b7-4f50-9db7-5e4202ad85ed)


Did you update the Klipper on your Pi, and now it is yelling at you about MCU version being out of date? Or maybe you just want to update the firmware on your boards for the latest features (or fixes). 
Either way, as long as your board is flashed with both Katapult *and* Klipper (as per the Initial Flashing section of this guide) you can just follow these steps and it should be pretty painless.

## Updating Klipper

Stop the Klipper service on the Pi by running:

```bash
sudo service klipper stop
```

Move into the klipper directory on the Pi by running:

```bash
cd ~/klipper
```

Then go into the klipper configuration menu by running:

```bash
make menuconfig
```

You can find screenshots of settings for common toolheads in the [Hardware Config](./hardware_config/hardware_config.md) section.

Otherwise, check the user manual for your board as it should list the proper klipper menuconfig settings.

Once you have the correct options selected, press Q to quit the menu (it will ask to save, choose yes).

You can now flash Klipper to your board using the existing *Klipper* /dev/serial ID you have in your printer.cfg file:

![image](https://github.com/user-attachments/assets/8db0e806-d664-455c-80f0-16d8d6770b16)

or you can find it by running `ls /dev/serial/by-id/*`

![image](https://github.com/user-attachments/assets/27097737-74b1-43d0-b7bf-3bdff2585375)

Then you can simply flash klipper using this device ID by running:

```bash
make flash FLASH_DEVICE=/dev/serial/by-id/usb-Klipper_your_board_id
```

![image](https://github.com/user-attachments/assets/c4be79f5-763e-4a55-8ea8-b91269f88adf)

![image](https://github.com/user-attachments/assets/62198289-dea3-441c-9c47-427050a1bf81)

Don't worry about the "CanBoot" or "CAN Flash Success", we aren't flashing anything CANBUS, this is just an idiosyncracy of the klipper make flash tool.

Klipper should now be successfully flashed. Double check that it still shows up as a Klipper device:

```bash
ls /dev/serial/by-id/*
```
![image](https://github.com/user-attachments/assets/27097737-74b1-43d0-b7bf-3bdff2585375)

Then start the Klipper service on the Pi again by running:

```bash
sudo service klipper start
```
