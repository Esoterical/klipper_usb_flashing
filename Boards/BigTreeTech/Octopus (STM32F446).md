# BigTreeTech Octopus

## Prerequisites

First, to make sure all the required dependencies are met, SSH into your Pi and run:

```bash
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-serial
```

## Installing Katapult via DFU Mode

Run the following commands to clone (or update) the repo:

```bash
test -e ~/katapult && (cd ~/katapult && git pull) || (cd ~ && git clone https://github.com/Arksine/katapult) ; cd ~
```

To configure the Katapult firmware, run these commands to change into the katapult directory and then modify the firmware menu:

```bash
cd ~/katapult
make menuconfig
```

Change the settings so it looks like this:

![image](https://github.com/Esoterical/voron_canbus/assets/124253477/673ce3c6-5bd7-48a8-bcd4-99aeefb0f0a2)

Press Q to quit the menu (it will ask to save, choose yes).

Compile the firmware with `make`. You will now have a katapult.bin at in your ~/katapult/out/katapult.bin.

To flash, connect the Octopus to the Pi via USB then put the octopus into DFU mode buy placing the boot jumper (purple) and pressing the reset button (green). The blue is for the "power over USB" jumper and isn't needed if you already have 24v hooked up to the octopus.

![image](https://user-images.githubusercontent.com/124253477/229234235-345ff23e-cc9e-4d61-ab7e-3df27dda1eb5.png)

To confirm it's in DFU mode you can run the command `lsusb` and look for an entry of "STMicroelectronics STM Device in DFU mode"

![image](https://github.com/user-attachments/assets/cde7138d-588b-4381-82ad-699cde37e0a8)

You can then flash the Katapult firmware to your mainboard by running

```bash
cd ~/katapult
make
sudo dfu-util -R -a 0 -s 0x08000000:leave -D ~/katapult/out/katapult.bin -d 0483:df11
```

If the result shows an "Error during download get_status" or something, but above it it still has "File downloaded successfully" then it still flashed OK and you can ignore that error.

![image](https://user-images.githubusercontent.com/124253477/225469341-46f3478a-aa96-4378-8d73-96faa90d561c.png)

Katapult should now be successfully flashed. Take your mainboard out of DFU mode (it might require removing jumpers and rebooting, or just rebooting). Check that Katapult is installed and by running 

```bash
ls /dev/serial/by-id
```

![image](https://github.com/Esoterical/voron_canbus/assets/124253477/1e9f0f7c-ada3-490b-bd62-bde25b67c362)

You should see a "usb-katapult_..." device there. If you don't, then double-click the RESET button on your board and `ls /dev/serial/by-id` again.

## Installing Klipper via Katapult

Move into the klipper directory on the Pi by running:

```bash
cd ~/klipper
```

Then go into the klipper configuration menu by running:

```bash
make menuconfig
```

Change the settings so it looks like this:

![image](https://github.com/user-attachments/assets/5bf92668-6ca6-47e5-8a77-f8bf50475cd0)

Press Q to quit the menu (it will ask to save, choose yes).

Compile the firmware with `make`. You will now have a klipper.bin in your ~/klipper/out/ folder.

Stop the Klipper service on the Pi by running:

```bash
sudo service klipper stop
```

Run an `ls /dev/serial/by-id/` and take note of the Katapult device that it shows:

![image](https://github.com/Esoterical/voron_canbus/assets/124253477/f836fa8d-fb26-4ccd-b1e1-50f010596852)

If the above command didn't show a 'katapult' device, or threw a "no such file or directory" error, then quickly double-click the RESET button on your mainboard and run the command again. Until you get a result from a `ls /dev/serial/by-id/` there is no point doing further steps below.

Run this command to install klipper firmware via Katapult via USB. Use the device ID you just retrieved in the above ls command.

```bash
python3 ~/katapult/scripts/flashtool.py -f ~/klipper/out/klipper.bin -d /dev/serial/by-id/usb-katapult_your_board_id
```

Klipper should now be successfully flashed. Check that it is installed and by running 

```bash
ls /dev/serial/by-id
```

![image](https://github.com/Esoterical/voron_canbus/assets/124253477/1e9f0f7c-ada3-490b-bd62-bde25b67c362)

You should see a "usb-klipper_..." device there instead of "usb-katapult_..."
