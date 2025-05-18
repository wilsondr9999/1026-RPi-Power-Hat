
## Introduction
This project is a HAT (hardware attached on top) for the Raspberry Pi, specifically designed for the RatRig V-Core4 3D printer.  This HAT adds some features to the printer that make the electronics wiring easier and more straightforward, and prevent certain problems that can occur with the original RatRig design.

![](img/1026%20RPi%20Power%20Hat%203D.png)

## Features
This HAT does the following:
- Removes the 5V power connection from the Octopus 3D printer control board that was used to power the Raspberry Pi, and replaces it with an on-board, high-current power regulator that can take 24V input directly.  This provides up to 20W (4A of 5V power) to the Raspberry Pi and all of its USB peripherals, rather than relying on the 5V regulator on the Octopus board.
- Provides an additional 4 USB ports to the Raspberry Pi using an on-board USB 2.0 hub IC.  This brings the total number of USB ports available for the 3D printer to 7 instead of 4.  The additional ports can support 2A of current each, with a total of 4A available to be shared among all 7 ports.
- Includes a small fan that cools the CPU on the Raspberry Pi.  The out-of-the-box design of the V-Core4 has a large fan to cool the entire electronics enclosure, but by default it only runs when the 3D printer's stepper motors are energized.  When the are not, it does not run, and this can cause the Raspberry Pi's temperature to increase into the 60C+ range.  The on-board fan will keep the Pi below 45C when the stepper motors are not running.

## Fabrication
You can have the PCB made at any PCB manufacturer.  The Gerber files are already prepared in the Fabrication Exports folder, the file is [1026 RPi Power Hat](KiCAD%20Project/Fabrication%20Exports/1026%20RPi%20Power%20Hat.zip), these are optimized and ready for submission to [OshPark](https://oshpark.com/).  If you want to modify the design, the KiCAD project is available in the KiCAD folder.  The PCB is a 4-layer design, your PCB manufacturer needs to support a minimum trace/space of 5 mil (0.127 mm).

For assembly, the recommended method is to use solder paste and a stencil with a reflow oven or hot air station.  The stencil can be made from the [1026 RPi Power Hat-F_Paste](KiCAD%20Project/Fabrication%20Exports/1026%20RPi%20Power%20Hat-F_Paste.gbr) file in the Fabrication Exports folder.  Inexpensive stencils are available from [OshStencils](https://www.oshstencils.com/#).

## Bill of Materials (BOM)
The bill of materials to assemble this project is available in the file [1026 RPi Power Hat](KiCAD%20Project/BOM/1026%20RPi%20Power%20Hat.csv).  Almost all electronic parts are available from Mouser or Digikey.  One exception is the two inductors (L1, L2), these are probably easiest to purchase directly from CoilCraft, the link is in the BOM file.  Some miscellaneous hardware can be purchased from Amazon, those links are also in the BOM file.

## Assembly - Speading Solder Paste for Reflow
To assemble the unit yourself, you will need a stencil and solder paste, along with a reflow oven or hot air station.  You can obtain the stencil as described above int he Fabrication section.

There is a solder stencil jig that can be 3D printed in the FreeCAD Project folder.  The file [1026 RPi Power Hat SSJ](FreeCAD%20Project/Solder%20Stencil%20Jig%20V2/1026%20RPi%20Power%20Hat%20SSJ.stl) (STL) can be imported into your preferred slicer and printed with the following settings:

- 0.2 mm layer height
- 0.4 mm nozzle
- 15% infill, use the Gyroid pattern
- PLA material

If you use PrusaSlicer, the file [1026 RPi Power Hat SSJ](FreeCAD%20Project/Solder%20Stencil%20Jig%20V2/1026%20RPi%20Power%20Hat%20SSJ.3mf) (3MF) already has these settings.  You most likely will have to adjust the print speeds for your printer, the speeds in the file are set for a RatRig V-Minion and are quite fast.

If you want to change aspects of the Solder Stencil Jig, the FreeCAD file is available named [Solder Stencil Jig V2](FreeCAD%20Project/Solder%20Stencil%20Jig%20V2/Solder%20Stencil%20Jig%20V2.FCStd), it is a parametric file that can generate a solder stencil jig for any PCB.

Once obtaining the manufactured PCB, the stencil, and printing the jig, you should have all 3 of them as such:

![](img/Stencil-PCB-Jig.jpg)

Insert the PCB into the solder stencil jig, the registration pins will go through the mounting holes:

![](img/PCB-Holder-Assembled.jpg)

Clean the PCB surface with isopropyl alcohol (99%), and clean the stencil the same way.  The PCB should look completely clean under a microscope, with no dust, hair, fibers, or oils on the PCB:

![](img/MS%20-%20Before%20Solder%20Paste.jpg)

Finally, place the stencil on top of the jig, two of the registration pins go through the stencil to align it:

![](img/Stencil-Holder-Assembled.jpg)

Spread the solder paste onto the stencil using a paste spreader or old plastic card.  Ensure the solder paste fills all openings in the stencil.  Remove the stencil, then carefully pop out the PCB from the jig.  **Do NOT leave the PCB in the jig while placing the components in the next step!**  The components will dislodge from the PCB when you pop it out later.

Your PCB pads should look like this after solder paste is applied:

![](img/MS%20-%20After%20Solder%20Paste.jpg)

## Assembly - Placing Components
Begin placing the surface mount components onto the PCB.  Start with the smallest components (0402 surface mount passives -- resistors, capacitors), and work up to the larger components.  Do not place any through-hole components at this stage.

You do not need to perfectly align every component, if the component leads are touching the solder paste on the correct pads and the component is flat, you're fine.  When the board is reflowed, the surface tension of the solder paste will pull the components into very good alignment with the pads.

Double- and Triple- check the polarity of the diodes, LEDs, and capacitors when you place them on the PCB, and check the pin 1 marker of all of the chips.  The silkscreen markings on the PCB match the mark on the component (provided you are using the exact component listed in the BOM).

The 0402 LEDs in particular are very difficult to identify which end is the cathode, so carefully check.

Unlike aluminum electrolytic capacitors where the negative terminal is marked, the tantalum polymer capacitors you will be soldering here have the positive terminal marked.  This matches the silkscreen on the PCB.

Once you get to the larger components, you need to carefully look at the pin alignment, especially on the big USB chip.  It is very easy to misalign the chip by one pin in any direction, so double-check it.

Your PCB should look like this after the components are placed:

![](img/MS%20-%20After%20Place%20Components.png)

## Assembly - Reflow
Reflow the PCB in a reflow oven using the solder paste manufacturer's recommended reflow profile.

If you are going to reflow with a hot air station, you need to be extremely careful with the heat level, as some components like the LEDs can melt if the temperature is too high.  Furthermore, the air flow needs to be low, as some of the very small 0402 components can be blown off the PCB.  If you have a PCB preheater, it will be very helpful here.

## Assembly - Through-Hole Components
Solder the through-hole components onto the PCB in the following order:
The following components are on the TOP side of the PCB, so we solder them on from the back side (bottom):
- 2x JST-XH-2 connectors for input power and the fan
- 1x USB-B connector for uplink
- 2x USB-A (2 port) connectors for downlink
The following component is on the BOTTOM side of the PCB, so we solder it on from the front side (top):
- 2x20 pin header

Look at the silkscreen marks on the PCB, they identify the side where the component goes.  Then you solder from the other side.

## Cleaning
It is recommended to clean the PCB after soldering to remove all remaining flux.  Isopropyl alcohol will remove it, but may require light brushing with a toothbrush, and may require multiple passes to remove all of the flux.  An ultrasonic cleaner with a detergent also works well if available.  Use only distilled water or isopropyl alcohol as solvents.

If you have used distilled water for rinsing or in an ultrasonic cleaner, dry the PCB using compressed air, and then further dry it in an oven at 125C for 2 hours.

Once you're finished, your PCB should look like this:

![](img/MS%20-%20After%20Clean.jpg)

## Fan Preparation
The fan that is to be installed on the PCB needs to have the JST-XH-2 connector (part number XHP-2) installed.  Cut the wires on the fan to a length of approximately 2 inches (5 cm), then crimp on two of the JST contacts (part number SXH-001T-P0.6).  Insert the crimped wire/contacts into the XHP-2 connector, pay attention to the required polarity.  The polarity is marked on the PCB, the fan's red wire goes to the positive (+) terminal on the PCB, this is the terminal closest to the M2.5 mounting screw hole.

Use the following picture as a reference for the fan wiring:

![](img/Fan%20Wiring.jpg)

Once the fan is terminated, attach it to the PCB using 3x M2.5 16mm hex cap screws and 3 M2.5 hex nuts on the underside of the PCB.  Ensure the fan is oriented correctly such that the air flow is from the top of the PCB through to the bottom of the PCB.  This will blow air onto the Raspberry Pi's CPU that is below.  For maximum effectiveness, add a passive heat sink to the Raspberry Pi's CPU chip.  There are two arrows on the side of the fan that show you both the rotation direction as well as the air flow direction, you can use these to assist you in orienting the fan in the correct position.

## Installation into the RatRig V-Core 4
Prepare a 2-wire power lead to go from the 24V power supply in the V-Core4 to the power HAT.  Terminate the ends of the lead on the 24V power supply side using connectors applicable to your power supply.

Terminate the HAT ends of the leads using a JST-XH-2 connector (part number XHP-2) the same way you did the fan.  Crimp on two of the JST contacts (part number SXH-001T-P0.6).  Insert the crimped wire/contacts into the XHP-2 connector, pay attention to the required polarity.  The polarity is marked on the PCB, the negative lead is on the side of the PCB's JST-XH-2 connector that is closest to the M2.5 mounting screw hole.

![](img/Power%20Input%20Wiring.jpg)

You will be assembling the HAT onto the top of your Raspberry Pi using 4 brass PCB standoffs (20mm length of the standoff + a 6 mm length of M2.5 threads) and 4 M2.5 x 6mm screws (pan-head phillips).  Use the following photo to see how the HAT is supposed to be mounted on top of the Raspberry Pi:

![](img/HAT%20Mounted.jpg)

Mount the HAT to the Raspberry Pi inside the V-Core4's electronics case.  The final result should look like this:

![](img/HAT%20Installed.jpg)

## USB Port Recommendations
Some of the USB devices on the RatRig V-Core4 have higher bandwidth requirements, and/or are more sensitive to issues than others.  Please use the following recommendations for which devices to plug where:

For all V-Core 4 models:
- Plug the USB-A to USB-B cable that connects the Raspberry Pi to the HAT using:
	- 1 USB-A 2.0 port on the Raspberry Pi (black plastic)
	- The USB-B port on the HAT

For CoreXY and Hybrid models:
- Toolhead / EBB42 board: Use a Raspberry Pi 3.0 (blue plastic) port
- Beacon Probe: Use a Raspberry Pi 3.0 (blue plastic) port
- Octopus Board: Use a Raspberry Pi 2.0 (black plastic) port
- Additional accessories, such as a chamber camera, nozzle camera, or touchscreen: Use a USB 2.0 port (black plastic) on the HAT

For IDEX models:
- Toolhead / EBB42 board 0: Use a Raspberry Pi 3.0 (blue plastic) port
- Toolhead / EBB42 board 1: Use the other Raspberry Pi 3.0 (blue plastic) port
- Beacon Probe: Use a Raspberry Pi 2.0 (black plastic) port
- Octopus Board: Use a USB 2.0 (black plastic) port on the HAT
- Additional accessories, such as a chamber camera, nozzle camera, or touchscreen: Use a USB 2.0 port (black plastic) on the HAT

## Initial Power-Up
At this point, if everything is connected, you can power on the V-Core4.  The HAT will provide the 5V power to the Pi through the GPIO header.  You should see the green power-on LED lit on the HAT.  If you see the red Fault LED lit up on the HAT, check your input voltage, it must be above 22V for the HAT to power on.  If the voltage checks out OK but you still get a fault LED, this may indicate that you have a short on the HAT PCB.  Re-check all soldered connections.

## Preparing the HAT in Linux
This HAT conforms to the Raspberry Pi HAT+ specification.  The HAT+ specification requires that the HAT contain an EEPROM with information that tells the Raspberry Pi what the HAT is and its capabilities.  We will program this EEPROM in the next steps.

### Transfer Required Files to the Pi
First, we will transfer the required files to the Raspberry Pi.  There are two files that need to be copied to the Raspberry Pi, they are in the Extras/Linux EEPROM Preparation folder.  The program that you can use to transfer these files from a Windows machine is [WinSCP](https://winscp.net/eng/download.php), available for free.  If you are using a Linux machine to connect to the Pi, scp is available on the command-line.

Using WinSCP, connect to the Raspberry Pi in your V-Core 4, and transfer the files [myhat](Extras/Linux%20EEPROM%20Preparation/myhat.eep) and [rr-vcore4-powerhat](Extras/Linux%20EEPROM%20Preparation/rr-vcore4-powerhat.dtbo) to your Raspberry Pi.  I recommend transferring these into the /home/pi directory.

The default username and password for the Raspberry Pi, if you have prepared it using RatRig's instructions, is "pi" and "raspberry".  If you have changed these, use your own username and password that you have established.

### Establish a Command Session to your Raspberry Pi
Using an SSH client like Putty, connect to your Raspberry Pi using it's IP address on port 22.  The default username and password is "pi" and "raspberry".

Once in the command terminal, execute the following commands to prepare the EEPROM:

``sudo -i
	>> The above command will again ask you for the password, the default is "raspberry".
``apt install cmake
``cd /root
``git clone https://github.com/raspberrypi/utils.git
``cd utils/eeptools
``cmake .
``make
``make install
``wget 
