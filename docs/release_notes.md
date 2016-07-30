# Release Notes

```
Release Notes (PN 93009415_C) 
Build 1.6.0
16 July, 2015

© 2015, Digi International
http://www.digi.com
```

## Introduction

This document provides the latest Release information for the Programmable XBee SDK, which allows customers to easily develop applications for programmable XBee modules inside the CodeWarrior IDE.

## Programmable XBee SDK v1.6.0, July 2015

### Supported Hardware and Software

#### Hardware

The Programmable XBee SDK currently supports following Digi Programmable XBee modules:

* XBee ZB (S2B)
	* 32KB flash memory
	* 128KB flash memory
* XBee ZB (S2C)
	* 32KB flash memory
* XBee ZB (S2CTH)
	* 32KB flash memory
* XBee 865/868LP DigiMesh (S8)
	* 32KB flash memory
* XBee 900HP DigiMesh (S3B)
	* 32KB flash memory

#### Software

The Programmable XBee SDK currently supports following host Operating Systems:

* Microsoft Windows XP/Vista/7/8

### Changes with respect to previous version

* **XBee Extensions:**
	* The XBee Extensions now support the XBee ZB (S2CTH) module.

* **XBee Firmware Library:**
	* Added Support for S2CTH module.
	* Improved power consumption on sleep mode.
	* Bug fixes:
		* Enabled pull-up in the pin that connects cpu-rx and radio-tx. Allows fast boot of S2CTH module
		* `sys_watchdog_reset()` is now called during banner to avoid watchdog reset when console is at 9600bps.
		* Fixed an issue that was causing the version string to be wrong in some scenarios.

### Known Issues and limitations

* The Virtual EEPROM is not currently supported by the 128KB module variants.
* Special considerations must be taken into account, regarding some special pins on the XBee ZB (S2B/S2C):
	* The RESET pin, when used as standard GPIO, has to be configured as input (due to a limitation of the 9S08QE).
	* The BKGD pin, when used as standard GPIO, has to be configured as output (due to a limitation of the 9S08QE).

## Programmable XBee SDK v1.5.5, December 2012

### Supported Hardware and Software

#### Hardware

The Programmable XBee SDK currently supports following Digi Programmable XBee modules:

* XBee ZB (S2B)
	* 32KB flash memory
	* 128KB flash memory
* XBee ZB (S2C)
	* 32KB flash memory
* XBee 865/868LP DigiMesh (S8)
	* 32KB flash memory
* XBee 900HP DigiMesh (S3B)
	* 32KB flash memory

#### Software

The Programmable XBee SDK currently supports following host Operating Systems:

* Microsoft Windows XP/Vista/7

### Changes with respect to previous version

* **XBee Extensions:**
	* The XBee Extensions now support the XBee 866/868LP DigiMesh and XBee 900 DigiMesh modules.
	* Added a new XBee Project Export wizard to export an existing project into a zip file.
	* Added a new XBee Project Import wizard to import an XBee project (previously exported with the corresponding wizard).
	* Added some extensions to the Smart Editor (Configuration tool):
		* The XBee Smart Editor now has a new page (accessible at any time from a tab at bottom) that displays a layout of the XBee module with information of the components associated to each XBee pin.
		* The XBee Smart Editor now supports “XBee pin templates” in the components. If a component has different pre-defined XBee pin configurations, you will be able to select the template to use in the Pins section of the Editor. The pins resolution process of editor should be able to change the selected template if necessary.
		* Now, if a component has dependent components in the project and you want to remove it, a dialog will offer you the possibility to remove also those dependent components.
		* Improved the usability and performance of the editor when adding, removing and editing components.
	* iDigi integration with the programmable XBee:
		* Added iDigi and XIG examples:
		* XIG LEDs. Shows how to manage 2 LEDs of an XBIB device remotely using the iDigi capabilities.
		* XIG Tanks. Shows how to remotely monitor and manage a tank emulated by a programmable XBee + an XBIB device.
		* New feature: Over The Air (OTA) firmware update. This feature allows you to update the application firmware of your programmable XBee from anywhere using the capabilities that the iDigi Device Cloud offers.
	* Documentation improvements:
		* New iDigi documentation section:
		* Added documentation explaining how to give iDigi connectivity to the programmable XBee modules using the XIG software.
		* Added documentation explaining how to update the radio firmware of the XBee devices through iDigi.
		* Documented how to perform an OTA firmware update through iDigi.
		* Updated the export/import XBee project documentation guide.
		* Added a new Getting Started Guide in the documentation for the Programmable XBee DigiMesh Development Kits.
		* Added documentation about the new view of the XBee Smart Editor.
		* Added a little guide explaining how to migrate a project from the 1.1 to the 1.5 version.
		* Included more tips in the Tips & Tricks section.

* **XBee Firmware Library:**
	* Added DigiMesh support to the library.
	* Updated the SPI component for the XBee ZB (S2C) module to include 2 pin templates.
	* Improved the IRQ component allowing the user to configure the pull-ups and pull-downs in those modules that support them. Also, fixed false edge detections during the GPIO configuration.
	* Improved the Power Management components allowing for keeping or not the uptime to save power.
	* Enabled the Low power voltage detection in the library. Added some settings (in the System and Power Management components) to manage it.
	* Updated the Bootloader example to version 37 (detects the new XBee module types). 
	* Added the following new samples:
		* **XBee DIO adapter ZB application** – The application shows some usage of the programmable XBee with the XBee DIO hardware.
		* **Low Voltage detection Example** – This example shows how to use the low power voltage detection feature.
		* **Serial Bypass** – Implements a bypass of the Freescale CPU inside the programmable XBee module.
		* **DigiMesh Unicast Demo** – Monitor. Implements the 'Monitor' side of the 'Digimesh Syncr Sleep power management' example.
		* **DigiMesh Unicast Demo** – Transmitter. Implements the 'Transmitter' side of the 'Digimesh Syncr Sleep power management' example.
		* **DigiMesh Broadcast Demo** – This application helps implementing a basic XBee network (from 2 to 5 XBee devices) in order to test the range each XBee covers and the ease integration of XBee modules running DigiMesh topology.
		* **DigiMesh Sleep Support** – Monitor. This example implements the same functionality than the DigiMesh Unicast Demo adding the Power Management feature.
		* **DigiMesh Sleep Support** – Transmitter. This example implements the same functionality than the DigiMesh Unicast Demo adding the Power Management feature.
		* **XIG LEDs and Buttons** – Specific example for the XIG integration. Allows for remotely manage 2 LEDs of the XBIB device. This example has both ZigBee and DigiMesh versions.
		* **XIG Tanks Simulation** – Specific example for the XIG integration. Allows for remotely monitor and manage an emulated liquid tank. This example has both ZigBee and DigiMesh versions.
		* **Sleeping Digital IRQ Sensor** – New Power Management example showing the IRQ wake up functionality.
		* **Adding a custom Digi's Endpoint Cluster** – Shows how to handle the reception of data sent to an specific Cluster in Digi Endpoint (E8). This example has both ZigBee and DigiMesh versions.
		* **Adding a custom endpoint** – Explains how to handle the reception of data sent to an specific endpoint which can have one or more clusters that will be implemented by the user. This example has both ZigBee and DigiMesh versions.
		* **Transmit Explicit Frames** – Application that shows how to use the XBee Communications library to build and send an explicit message to other device. This example has both ZigBee and DigiMesh versions.
		* **Simple Chat with NI** – Similar to the Simple Chat, but the destination is automatically found.
		* Ported the following examples to be DigiMesh compatible: “Set and get a Remote XBee device AT parameters”, “Simple Chat” and “Transparent Client”.
	* Synchronization with the XBee driver API (mainly for DigiMesh support).
	* Added the programming guide sections for the following components:
		* I2C
		* GPIO IRQ
		* GPIO Ports
		* UART
		* System
	* Added a PC application (host) for the OTA firmware update which replaces the X-CTU manual process of the OTA example.
	* Generalization of the frame receive process, now all the received frames are explicit (AO = 3). This change is transparent for the user.
	* The Over the Air (OTA) firmware update is now a service of the XBee Firmware Library and can be configured under the ZigBee or DigiMesh configuration component.
	* General improve of the DigiMesh and ZigBee components, callbacks generated, code snippets added, etc.
	* Improved the boot sequence of the applications.
	* General bug fixing.

### Known Issues and limitations

* The Virtual EEPROM is not currently supported by the 128KB module variants.
* Special considerations must be taken into account, regarding some special pins on the XBee ZB (S2B/S2C):
	* The RESET pin, when used as standard GPIO, has to be configured as input (due to a limitation of the 9S08QE).
	* The BKGD pin, when used as standard GPIO, has to be configured as output (due to a limitation of the 9S08QE).
