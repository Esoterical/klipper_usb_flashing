---
layout: default 
title: Initial Flashing for STM32 Boards
has_children: false
nav_order: 20
has_toc: false
---

# Initial Flashing for STM32-based Boards

The following should be taken as an overall guide on what you are going to be achieving.

**PLEASE DO NOT TAKE THE SCREENSHOTS/CONFIGURATIONS ON THIS PAGE EXACTLY AS WRTTEN AS THEY MAY NOT BE COMPATIBLE WITH YOUR PARTICULAR MAINBOARD**

First, to make sure all the required dependencies are met, SSH into your Pi and run:

```bash
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-serial
```

## Installing Katapult via DFU Mode

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

![image](https://github.com/Esoterical/voron_canbus/assets/124253477/5434691f-2d97-4d75-9067-d7501c2a2214)

Press Q to quit the menu (it will ask to save, choose yes).

Compile the firmware with `make`. You will now have a katapult.bin at in your ~/katapult/out/katapult.bin.

To flash, connect your board to the Pi via USB then put the board into DFU mode (this should be included in the hardware_config section for your board, but if it's not then the user manual from the manufacturer should have the instructions). 

To confirm it's in DFU mode you can run the command `lsusb` and look for an entry of "STMicroelectronics STM Device in DFU mode"

![image](https://github.com/user-attachments/assets/cde7138d-588b-4381-82ad-699cde37e0a8)

You can then flash the Katapult firmware to your mainboard by running

```bash
cd ~/katapult
make
sudo dfu-util -R -a 0 -s 0x08000000:mass-erase:force:leave -D ~/katapult/out/katapult.bin -d 0483:df11
```

If the result shows an "Error during download get_status" or something, but above it it still has "File downloaded successfully" then it still flashed OK and you can ignore that error.

{: .highlight }
> If you get a different error and do **not** see a "File downloaded successfully" then try:
>
> `sudo dfu-util -R -a 0 -s 0x08000000:leave -D ~/katapult/out/katapult.bin -d 0483:df11`
>

![image](https://user-images.githubusercontent.com/124253477/225469341-46f3478a-aa96-4378-8d73-96faa90d561c.png)

Katapult should now be successfully flashed. Take your mainboard out of DFU mode (it might require removing jumpers and rebooting, or just rebooting). Check that Katapult is installed and by running 

```bash
ls /dev/serial/by-id/*
```

![image](https://github.com/user-attachments/assets/7931fa4d-ebe1-454d-b8dc-a36e73fff727)


You should see a "usb-katapult_..." device there. If you don't, then double-click the RESET button on your board and `ls /dev/serial/by-id` again.

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

![image](https://github.com/user-attachments/assets/230b3c37-73da-4198-91eb-3f64e9678678)

![image](https://github.com/user-attachments/assets/62198289-dea3-441c-9c47-427050a1bf81)


Don't worry about the "CanBoot" or "CAN Flash Success", we aren't flashing anything CANBUS, this is just an idiosyncracy of the klipper make flash tool.

Klipper should now be successfully flashed. Check that it is installed and by running 

```bash
ls /dev/serial/by-id/*
```
![image](https://github.com/user-attachments/assets/27097737-74b1-43d0-b7bf-3bdff2585375)

You should see a "usb-klipper_..." device there instead of "usb-katapult_..."

Use this USB ID in the [mcu] section of your printer.cfg in order for Klipper (on Pi) to connect to the mainboard. (If this is a secondary board, like a second SKR for Z motors, or a Toolhead board, then make sure to name the mcu section, [mcu some_name] as per the [Klipper docs](<https://www.klipper3d.org/Config_Reference.html#mcu-my_extra_mcu>)).

![image](https://github.com/user-attachments/assets/8db0e806-d664-455c-80f0-16d8d6770b16)


Start the Klipper service on the Pi again by running:

```bash
sudo service klipper start
```

# Finished

You have now successfully flashed both Katapult and Klipper to your board.
