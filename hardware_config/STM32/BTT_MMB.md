---
layout: default 
title: BigTreeTech MMB
parent: Hardware Configurations
---

The following settings are valid for the MMB v1.0, v1.1, and v2.0

# DFU Mode
1.  Add a jumper as shown in the image below so the board can be powered via a USB connection
    ![image](https://github.com/Esoterical/voron_canbus/assets/124253477/c5f00b2a-c6dc-4f80-b9aa-4b963d21a580)


2. Connect your device to your Pi via USB
3. Press and hold the `Reset` and `BOOT` buttons down (button locations shown in step 1)
    1. Release `Reset` button
    2. Release `BOOT` button
4. The device should now be in DFU mode. Verify this via the `lsusb` command, which should look something like this:
    ```
    Bus 001 Device 005: ID 0483:df11 STMicroelectronics STM Device in DFU Mode
    ```

# Katapult Config

![image](https://github.com/user-attachments/assets/62caa197-cc8d-4ece-8435-e81b1d625cb4)



# Klipper Config

![image](https://github.com/user-attachments/assets/8a9546af-b3a1-4ec7-9e4f-9d92503d8e3c)



# Sample Configuration

A sample configuration file can be found at [https://github.com/bigtreetech/MMB/tree/master/Firmware
](https://github.com/bigtreetech/MMB/tree/master/Firmware
)
