---
layout: default 
title: BigTreeTech EBB36 Gen2
parent: Hardware Configurations
---

# USB Mode

To put the EBB36 Gen2 into USB mode (instead of CAN mode) make sure to **remove** the jumper on the USB/CAN header

<img width="1015" height="559" alt="image" src="https://github.com/user-attachments/assets/767bf8fb-bab9-4a29-82b2-96e6b2bf10e3" />


# DFU Mode

To put the EBB36 Gen2 into DFU mode first power off the printer then connect the main CAN/Power cable from the EBB36 Gen2 to the breakout board that goes in your electronics bay.

Then make sure you have power connected to this breakout board as well, and then connect a USB cable from your Pi to the breakout board. 

Then power up the system and on the EBB36 Gen2 board hold the BOOT button, press and release the RST button, then count to 5 and release the BOOT button.

<img width="1365" height="671" alt="image" src="https://github.com/user-attachments/assets/2b0bf37d-0bbd-4aa2-8c0c-7b3fe2742544" />


# Katapult Config

<img width="754" height="274" alt="image" src="https://github.com/user-attachments/assets/af504c9a-43db-487f-b018-64ebe42ab554" />


# Klipper Config

<img width="717" height="238" alt="image" src="https://github.com/user-attachments/assets/a6c27dec-c665-49af-b764-c8d7ccc1b10f" />



# Sample Configuration

A sample configuration file can be found at [https://github.com/bigtreetech/EBB/blob/master/EBB_GEN2/EBB36_GEN2/sample-bigtreetech-ebb36-gen2-v1.0.cfg](https://github.com/bigtreetech/EBB/blob/master/EBB_GEN2/EBB36_GEN2/sample-bigtreetech-ebb36-gen2-v1.0.cfg)
