---
layout: default 
title: Initial Flashing for RP2040 Boards
has_children: false
nav_order: 30
has_toc: false
---

# Initial Flashing for RP2040-based Boards

The following should be taken as an overall guide on what you are going to be achieving.

**PLEASE DO NOT TAKE THE SCREENSHOTS/CONFIGURATIONS ON THIS PAGE EXACTLY AS WRTTEN AS THEY MAY NOT BE COMPATIBLE WITH YOUR PARTICULAR MAINBOARD**

First, to make sure all the required dependencies are met, SSH into your Pi and run:

```bash
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-serial
```

## Installing Katapult via RP Boot Mode

First you need to clone the Katapult repo onto your pi. Run the following commands to clone (or update) the repo:

```bash
test -e ~/katapult && (cd ~/katapult && git pull) || (cd ~ && git clone https://github.com/Arksine/katapult) ; cd ~
```

To configure the Katapult firmware, run these commands to change into the katapult directory and then modify the firmware menu:

```bash
cd ~/katapult
make menuconfig
```

You will need to adapt the below instructions so they cover _your_ board's specicific configuration. You can find screenshots of settings for common toolheads in the [Hardware Config](./hardware_config/hardware_config.md) section.

If your board doesn't exist in the hardware_config folder already, then you want the Processor, Clock Reference, and Application Start offset to be set as per whatever board you are running. Set the "Build Katapult deployment application" (this is really only for updating but doesn't hurt having it enabled at this stage), and make sure "Communication Interface" is set to USB. Also make sure the "Support bootloader entry on rapid double click of reset button" is marked. It makes it so a double press of the reset button will force the board into Katapult mode. Makes re-flashing after a mistake a lot easier. Lastly, setting the Status LED GPIO Pin won't affect how katapult functions, but it will give a nice visual indicator (of an LED flashing on and off once a second) on the toolhead to show the board is sitting in Katapult mode.

![image](https://github.com/user-attachments/assets/e60a9ffc-5e64-4f00-9b82-0e447ac5db8a)

Press Q to quit the menu (it will ask to save, choose yes).

Compile the firmware with `make`. You will now have a katapult.bin at in your ~/katapult/out/katapult.bin.

To flash, connect your board to the Pi via USB then put the board into RP Boot mode (this should be included in the hardware_config section for your board, but if it's not then the user manual from the manufacturer should have the instructions). 

To confirm it's in RP Boot mode you can run the command `lsusb` and look for an entry of Raspberry Pi RP2 Boot"

![image](https://github.com/user-attachments/assets/4a0338dd-06b2-4415-a834-a5cc18eb0d0a)

**Note**
Older linux distributions may not show the name entirely, but if you see an entry with ID 2e8a:0003 and no name this is fine too and means your board is in boot mode.

![image](https://github.com/user-attachments/assets/9cdabe2b-7cca-4707-9375-631a93a98e16)


You can then flash the Katapult firmware to your mainboard by running

```bash
cd ~/katapult
make
make flash FLASH_DEVICE=2e8a:0003
```

![image](https://github.com/user-attachments/assets/7fe1ef45-e628-4742-8be3-05ce8699fd5c)

Katapult should now be successfully flashed. Check that Katapult is installed by running 

```bash
ls /dev/serial/by-id/*
```

![image](https://github.com/user-attachments/assets/27cca753-6f22-4888-900a-63dfe7877b7c)


You should see a "usb-katapult_..." device there. If you don't, then double-click the RESET button on your board (if your board has a reset button) and `ls /dev/serial/by-id` again. Otherwise you may have to put the board back into RP Boot mode and try flashing Katapult to it again (and check your menuconfig settings are correct).

## Installing Klipper via Katapult

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

Again, if your mainboard is already in [Hardware Config](./hardware_config/hardware_config.md) then you can copy the Klipper settings from there. 

Otherwise, check the user manual for your board as it should list the proper klipper menuconfig settings.

Once you have the correct options selected, press Q to quit the menu (it will ask to save, choose yes).

You can now flash Klipper to your board using the Katpult /dev/serial ID you found earlier by running:

```bash
make flash FLASH_DEVICE=/dev/serial/by-id/usb-katapult_your_board_id
```
![image](https://github.com/user-attachments/assets/135ee47e-aa1f-42e0-9dc9-70e9188a5117)

![image](https://github.com/user-attachments/assets/bffb882d-145a-40c7-abb6-dc6247f11a88)

Don't worry about the "CanBoot" or "CAN Flash Success", we aren't flashing anything CANBUS, this is just an idiosyncracy of the klipper make flash tool.

Klipper should now be successfully flashed. Check that it is installed and by running 

```bash
ls /dev/serial/by-id/*
```

![image](https://github.com/user-attachments/assets/d661fdce-b475-45e2-87be-60e4a8fd09ce)

You should see a "usb-klipper_..." device there instead of "usb-katapult_..."

Use this USB ID in the [mcu] section of your printer.cfg in order for Klipper (on Pi) to connect to the mainboard. (If this is a secondary board, like a second SKR for Z motors, or a Toolhead board, then make sure to name the mcu section, [mcu some_name] as per the [Klipper docs](<https://www.klipper3d.org/Config_Reference.html#mcu-my_extra_mcu>)).

![image](https://github.com/user-attachments/assets/f9b42ab5-4da8-46de-86e1-60e8b8dfd98a)


Start the Klipper service on the Pi again by running:

```bash
sudo service klipper start
```

# Finished

You have now successfully flashed both Katapult and Klipper to your board.
