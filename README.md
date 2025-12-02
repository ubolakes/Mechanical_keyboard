[comment]: <> (Author:  Umberto Laghi)
[comment]: <> (Contact: ul2509@gmail.com)
[comment]: <> (Github:  @ubolakes)

# :warning: WORK IN PROGRESS :warning:

# *La Jaderissima* mechanical keyboard
[![Apache 2.0 license](https://img.shields.io/badge/license-Apache%202-blue)](LICENSE)

*La Jaderissima* is an open source mechanical keyboard designed with the intent to learn how to design a PCB.  
The repository contains all the materials necessary to build your own *La Jaderissima* at home.

Before introducing the project in more detail, I'd like to thank my friend and colleague, Biagio M., who designed the keyboard case using a 3D CAD software. Without him, I wouldn't have been able to make it.  
He also made the design as thin as possible due to my childish complaints about wanting the keyboard to be as close to the desk as possible.

[comment]: <> (TODO: add image of the final product)

## General overview
The keyboard is designed with a 96% ANSI layout to provide all the necessary keys while reducing the footprint compared to a 100% layout.

<div align="center" style="text-align: center; margin-left: auto; margin-right: auto;">
  <img src="./source/images/keyboard-layout.jpg" alt="Keyboard layout" width="700px">

*Figure 1: Mechanical keyboard layout*
</div>

## Case design
The feature I desire most in a keyboard is a thin design that reduces wrist fatigue without the need for a wrist rest. A slimmer keyboard also offers a sleeker look (I guess).

To achieve this, my friend and colleague, Biagio, designed a bent sheet metal backplate and a 3D-printable bottom case in order to reduce costs and make the keyboard lighter. Biagio also designed 3D-printable feet to angle the keyboard and improve ergonomics.

[comment]: <> (TODO: add render of the two case pieces from CAD)

## Keyswitch
Another design choice that makes the keyboard thinner is the use of low-profile switches. It was difficult to choose the most suitable keyswitch.

The first type of switch I chose was the Kailh Choc. The problem with them is that they are a completely custom design. Finding keycaps, stabilizers, and mechanical drawings to understand the dimensions was difficult and expensive.

After my search, I discovered the Outemu GTMX medium-profile switches. They have a lower profile than Cherry MX switches, but not as low as Kailh Choc switches. They have the same footprint as standard Cherry MX switches and are compatible with MX-specific PCBs, backplates, keycaps, and MX PCB-mounted stabilizers, which allows for a lower price.

<div align="center" style="text-align: center; margin-left: auto; margin-right: auto;">
  <img src="./source/images/MX-vs-GTMX.png" alt="MX and GTMX heights compared" width="300px">

*Figure 2: Cherry MX and Outemu GTMX heights compared*
</div>

[comment]: <> (TODO: add section with the BOM)

[comment]: <> (TODO: add files  for PCBWAY [and/or AISLER] and Laserboost)

## How to build your own

### PCB
[comment]: <> (TODO: add image of the PCB)

You can build a PCB yourself using the files in the .zip folder, which contains everything the fabricator needs.
You can choose any fabricator, since most of them accept source files exported from KiCAD.

Along with the PCB, you will need hotswap sockets for MX switches. I chose the Kailh ones, but I think these are pretty much standardised.

You will also need diodes to prevent current from flowing in the wrong direction and to avoid unintentional clicks. The specific type of diode required is the 1N4148; these are cheap and easy to obtain.

### Switches
You can mount any type of mechanical switch as long as it is MX compatible.
For the stabilizers, you can choose PCB-mounted or plate-mounted ones, as the PCB has holes for them and the plate is designed to hold stabilizers.

[comment]: <> (TODO: add section about stabs)

### Keycaps
As long as they use an ANSI layout, you can choose any type of keycap.
I chose a low-profile set to maintain a short profile.

### Case
The case can be 3D-printed in any material or color you prefer.
Since I used a standard 3D printer, I had to split the case into two parts to fit the printer's build plate. I used two 4x16 mm plugs and four 3x16 mm plugs to join them; you can also add glue to better keep the pieces together.

If you have access to a 3D printer with a larger footprint, I included a step file so you can print the case in one piece and avoid using plugs.

Since you are a skilled 3D designer, I also included the CAD file of the keyboard PCB with switches so that you can design your own case with all the features you desire.

[comment]: <> (TODO: add CAD files for the case: split version and integral)
[comment]: <> (TODO: add image of the 3d printed case)

### MCU
I decided to use a Raspberry Pi Pico as the MCU for the mechanical keyboard because it's inexpensive, can be mounted using connector pins, and has plenty of GPIO to handle the entire keyboard.
While an original RPi Pico is not necessary, as they could be more expensive, any Chinese clone is fine as long as it has the same pinout and an RP2040 MCU.

### Firmware
[comment]: <> (TODO: add guide on how to flash the firmware)
The firmware was developed using QMK, and it can be flashed on an RP2040 MCU. Otherwise, it would not work.

To compile and flash the firmware on your La_Jaderissima keyboard, you need to install the QMK environment. The following steps are specifically for a GNU/Linux operating system (OS). If you are using a different OS, you can follow the specific guide on the QMK website.

1. Install the QMK CLI
```
curl -fsSL https://install.qmk.fm | sh
```
2. Download the fork containing La_Jaderissima firmware
```
qmk setup ubolakes/La_Jaderissima_qmk_firmware
```
3. Connect the RPi Pico via USB and go into bootloader mode
4. Build and flash the firmware on the MCU
```
qmk flash -kb la_jaderissima -km default
```

If everything worked fine you now have a RPi Pico with La_Jaderissima firmware flashed.