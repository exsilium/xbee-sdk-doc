<h1>2. API Reference</h1>

The API Reference is a Doxygen generated documentation set which is readable via Github Pages: [http://exsilium.github.io/xbee-sdk-doc/](http://exsilium.github.io/xbee-sdk-doc/)

# 2.1 Overview

The XBee Firmware Library is an extensive and specific API provided to facilitate the development of programmable XBee applications.

## Overview of XBee interfaces and functional modules

* [1-Wire](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire.html)
	* [1-Wire driver](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__driver.html)
	* [1-Wire components](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__components.html)
		* [DS18B20 digital thermometer](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__ds18b20.html)
        * [DS1904 Real-Time Clock](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__ds1904.html)

* [Analog Digital Converter (ADC)](http://exsilium.github.io/xbee-sdk-doc/group__api__adc.html)

* [CPU Drivers](http://exsilium.github.io/xbee-sdk-doc/group__api__cpu.html)
	* [Flash](http://exsilium.github.io/xbee-sdk-doc/group__cpu__flash.html)
    * [Power Management (PM)](http://exsilium.github.io/xbee-sdk-doc/group__cpu__pm.html)
    * [System](http://exsilium.github.io/xbee-sdk-doc/group__cpu__system.html)
    * [Low-Voltage Detection (LVD)](http://exsilium.github.io/xbee-sdk-doc/group__api__lvd.html)

* [EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__eeprom.html)
	* [24xxx EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__24xxx__eeprom.html)
    * [25AAxxxx/25LCxxxx EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__25xxx__eeprom.html)
    * [Virtual EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__virtual__eeprom.html)

* [General Purpose Input/Output (GPIO)](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios.html)
	* [Standard GPIO](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios__gpio.html)
    * [Interrupt ReQuest Control (IRQ)](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios__irq.html)
    * [Port](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios__port.html)

* [High Resolution Timer](http://exsilium.github.io/xbee-sdk-doc/group__api__timer.html)

* [Input Capture component](http://exsilium.github.io/xbee-sdk-doc/group__api__input__capture.html)

* [Inter-Integrated Circuit (I2C)](http://exsilium.github.io/xbee-sdk-doc/group__api__i2c.html)

* [Output Compare component](http://exsilium.github.io/xbee-sdk-doc/group__api__output__compare.html)

* [Pulse-Width Modulation (PWM)](http://exsilium.github.io/xbee-sdk-doc/group__api__pwm.html)

* [Real Time Clock (RTC)](http://exsilium.github.io/xbee-sdk-doc/group__api__rtc.html)

* [Serial Peripheral Interface (SPI)](http://exsilium.github.io/xbee-sdk-doc/group__api__spi.html)

* [Universal Asynchronous Receiver-Transmitter (UART)](http://exsilium.github.io/xbee-sdk-doc/group__api__uart.html)

Apart from the internal modules and interfaces, the XBee Firmware Library provides also drivers for some external devices that can be connected and managed by the XBee module:

* [LCD Display (SPI)](http://exsilium.github.io/xbee-sdk-doc/group__api__display__graphic.html)

* [Character LCD](http://exsilium.github.io/xbee-sdk-doc/group__api__char__lcd.html)

* [Capacitive Board (I2C)](http://exsilium.github.io/xbee-sdk-doc/group__mpr121__keyboard.html)

Other references to the Firmware Library:

*   [Types](http://exsilium.github.io/xbee-sdk-doc/group__types.html)

## Overview of Cross-Platform, ANSI C, XBee/ZigBee Driver

The driver is broken up into multiple layers, with well-defined interfaces between each layer.

The two parts of the driver are similar to an Ethernet NIC driver and a TCP/IP networking stack. In our case, the [XBee Driver](group__xbee.html) handles all serial communication with and configuration of the attached XBee device, the [Wireless Personal Networking](group__wpan.html) layer provides generic 802.15.4 networking support (endpoints and clusters), and the [ZigBee Networking Stack](group__zigbee.html) layer provides support for the ZigBee networking protocols.

These layers make use of a [Hardware Abstraction Layer](group__hal.html) that must be created for each hardware/compiler platform.

See the [Modules ]() section for a full outline of the API layers.

## WPAN Overview

### Endpoint Table

The endpoint table is a complex data structure that describes all endpoints, clusters, ZCL attributes and manufacturer-specific command handlers for a given device. The structure of the table is as follows (note that not all members of each object are listed):

* Each DEVICE ([wpan_dev_t](http://exsilium.github.io/xbee-sdk-doc/structwpan__dev__t.html)) corresponds to a local, serially-connected XBee module. This DEVICE has multiple ENDPOINTs.
* Each ENDPOINT ([wpan_endpoint_table_entry_t](http://exsilium.github.io/xbee-sdk-doc/structwpan__endpoint__table__entry__t.html "Information on each endpoint on this device.")) has
	* An ENDPOINT ID (0 to 254), PROFILE ID, DEVICE ID and DEVICE VERSION.
    * Multiple CLUSTERs. The ZDP endpoint handler currently uses a switch to handle frames for each cluster, but could be updated to let the endpoint dispatcher hand frames off to each cluster's handler.
    * A HANDLER to process frames for CLUSTERs without their own HANDLER, or CLUSTERs that aren't in the table.
    * A pointer to an ENDPOINT STATE ([wpan_ep_state_t](http://exsilium.github.io/xbee-sdk-doc/structwpan__ep__state__t.html)) structure.

* Each CLUSTER ([wpan_cluster_table_entry_t](http://exsilium.github.io/xbee-sdk-doc/structwpan__cluster__table__entry__t.html "Information on each cluster associated with an endpoint.")) has
	* FLAGs indicating whether it is an input or output cluster (or both), and whether packets sent to/from the cluster require APS-layer encryption.
    * A HANDLER to process frames for that cluster.
    * A CONTEXT pointer that is passed to the HANDLER. For a ZCL endpoint, the CONTEXT points to an ATTRIBUTE TREE.

* On ZCL endpoints, each entry in the ATTRIBUTE TREE ([zcl_attribute_tree_t](http://exsilium.github.io/xbee-sdk-doc/structzcl__attribute__tree__t.html)) has
	* A manufacturer ID with ZCL_MFG_NONE (0) representing the general attributes for the cluster.
    * Pointers to a list of SERVER and CLIENT cluster ATTRIBUTEs.

* Each ATTRIBUTE is either a BASE ATTRIBUTE ([zcl_attribute_base_t](http://exsilium.github.io/xbee-sdk-doc/structzcl__attribute__base__t.html)) with
	* A 16-bit ID.
    * FLAGS indicating whether the attribute is read-only, is a full attribute (see below), has a minimum or maximum limit and is reportable.
    * A ZCL TYPE.
    * A pointer to the ATTRIBUTE's VALUE.

* ... or a FULL ATTRIBUTE ([zcl_attribute_full_t](http://exsilium.github.io/xbee-sdk-doc/structzcl__attribute__full__t.html)) which has
	* A BASE ATTRIBUTE structure (so both BASE and FULL attributes start with the same structure elements).
    * Optional MINIMUM and MAXIMUM ([zcl_attribute_minmax_t](http://exsilium.github.io/xbee-sdk-doc unionzcl__attribute__minmax__t.html "Used for #ZCL_CMD_DEFAULT_RESP.")) values.
    * A READ function (zcl_attribute_update_fn) to refresh the ATTRIBUTE's VALUE.
    * A WRITE function (zcl_attribute_write_fn) to process a ZCL Write Attributes request if the attribute requires additional processing over what the standard function, zcl_decode_attribute, does.
    
### Endpoint Dispatching

The endpoint dispatcher searches the endpoint table to find a handler for a given frame, based on its destination endpoint and cluster ID.

## ZigBee Overview

### ZDO/ZDP (ZigBee Device Object/Profile) Command Processing

The ZDO endpoint handler (registered to endpoint 0) walks the endpoint table to respond to requests. It needs to know about all endpoints and their input clusters and output clusters. It walks the endpoint table but stops at the context elements. Therefore, all information required by the ZDO layer must exist outside of the context elements of the endpoint table.

### ZCL (ZigBee Cluster Library) Command Processing

Consider a theoretical cluster with manufacturer-specific attributes and commands for more than one manufacturer ID. The handler registered to that cluster would check the frame type and manufacturer-specific bits and hand any GENERAL/PROFILE or MANUFACTURER-SPECIFIC commands off to the ZCL General Command Handler (zcl_general_command).

### ZCL General Command Handler

This handler will see frames from the endpoint dispatcher for

* Clusters that aren't in the cluster table for the endpoint (invalid clusters).
* Clusters that don't have their own handler (no cluster commands).

It also receives frames from clusters with handlers for cluster-specific commands that are passing on a general or manufacturer-specific command frame.

The ZCL General Command handler finds the correct attribute list from the attribute tree (general vs. manufacturer-specific, server vs. client cluster), and then

* If the frame is marked CLUSTER &amp; MANUFACTURER-SPECIFIC, it passes the frame on to the handler for that MFG ID (stored in the attribute tree).
* If it is marked CLUSTER-SPECIFIC but GENERAL, it generates an error.
* If it is marked PROFILE-SPECIFIC and GENERAL, it processes the frame as a general command, using the attribute list it retreived from the tree.

### Summary of ZCL handlers

* ZCL General Command handler registered to the endpoint to process frames for invalid clusters or clusters without cluster-specific commands (i.e., clusters with a NULL command handler).
* Cluster-specific, general command handler registered to each cluster.
* Cluster-specific, manufacturer-specific command handler(s) listed in the attribute tree (stored in the cluster structure's context member) under the appropriate manufacturer ID.

# 2.2 Modules

Here is a list of all modules:

* [1-Wire](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire.html)
	* [1-Wire components](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__components.html)
		* [DS18B20 digital thermometer](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__ds18b20.html)
        * [DS1904 Real-Time Clock](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__ds1904.html)
	* [1-Wire driver](http://exsilium.github.io/xbee-sdk-doc/group__api__1__wire__driver.html)
* [Analog Digital Converter (ADC)](http://exsilium.github.io/xbee-sdk-doc/group__api__adc.html)
* [CPU Drivers](http://exsilium.github.io/xbee-sdk-doc/group__api__cpu.html)
	* [Flash](http://exsilium.github.io/xbee-sdk-doc/group__cpu__flash.html)
    * [Low-Voltage Detection (LVD)](http://exsilium.github.io/xbee-sdk-doc/group__api__lvd.html)
    * [Power Management (PM)](http://exsilium.github.io/xbee-sdk-doc/group__cpu__pm.html)
    * [System](http://exsilium.github.io/xbee-sdk-doc/group__cpu__system.html)
* [Capacitive Board (I2C)](http://exsilium.github.io/xbee-sdk-doc/group__mpr121__keyboard.html)
* [Character LCD](http://exsilium.github.io/xbee-sdk-doc/group__api__char__lcd.html)
* [EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__eeprom.html)
	* [24xxx EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__24xxx__eeprom.html)
    * [25AAxxxx/25LCxxxx EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__25xxx__eeprom.html)
    * [Virtual EEPROM](http://exsilium.github.io/xbee-sdk-doc/group__api__virtual__eeprom.html)
* [General Purpose Input/Output (GPIO)](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios.html)
	* [Interrupt ReQuest Control (IRQ)](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios__irq.html)
    * [Port](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios__port.html)
    * [Standard GPIO](http://exsilium.github.io/xbee-sdk-doc/group__api__gpios__gpio.html)
* [Hal_hcs08](http://exsilium.github.io/xbee-sdk-doc/group__hal__hcs08.html)
* [Hardware Abstraction Layer (HAL)](http://exsilium.github.io/xbee-sdk-doc/group__hal.html)
	* [DOS16/OpenWatcom](http://exsilium.github.io/xbee-sdk-doc/group__hal__dos.html)
    * [Freescale/Codewarrior (Programmable XBee)](http://exsilium.github.io/xbee-sdk-doc/group__hal__freescale.html)
    * [Rabbit/Dynamic C](http://exsilium.github.io/xbee-sdk-doc/group__hal__rabbit.html)
    * [Win32/cygwin/gcc](http://exsilium.github.io/xbee-sdk-doc/group__hal__win32.html)
* [High Resolution Timer](http://exsilium.github.io/xbee-sdk-doc/group__api__timer.html)
* [Input Capture component](http://exsilium.github.io/xbee-sdk-doc/group__api__input__capture.html)
* [Inter-Integrated Circuit (I2C)](http://exsilium.github.io/xbee-sdk-doc/group__api__i2c.html)
* [LCD Display (SPI)](http://exsilium.github.io/xbee-sdk-doc/group__api__display__graphic.html)
* [Miscellaneous functions](http://exsilium.github.io/xbee-sdk-doc/group__api__misc.html)
* [Output Compare component](http://exsilium.github.io/xbee-sdk-doc/group__api__output__compare.html)
* [Pulse-Width Modulation (PWM)](http://exsilium.github.io/xbee-sdk-doc/group__api__pwm.html)
* [Real Time Clock (RTC)](http://exsilium.github.io/xbee-sdk-doc/group__api__rtc.html)
* [Rtc_freescale](http://exsilium.github.io/xbee-sdk-doc/group__rtc__freescale.html)
* [Serial Peripheral Interface (SPI)](http://exsilium.github.io/xbee-sdk-doc/group__api__spi.html)
* [Types](http://exsilium.github.io/xbee-sdk-doc/group__types.html)
* [Universal Asynchronous Receiver-Transmitter (UART)](http://exsilium.github.io/xbee-sdk-doc/group__api__uart.html)
* [Utility/Support Code](http://exsilium.github.io/xbee-sdk-doc/group__util.html)
	* [Byte-swapping functions](http://exsilium.github.io/xbee-sdk-doc/group__util__byteorder.html)
    * [Circular Buffer](http://exsilium.github.io/xbee-sdk-doc/group__util__cbuf.html)
    * [XMODEM code used by the firmware update process](http://exsilium.github.io/xbee-sdk-doc/group__util__xmodem.html)
* [Wireless Personal Area Networking (WPAN)](http://exsilium.github.io/xbee-sdk-doc/group__wpan.html)
	* [Cluster/Endpoint layer](http://exsilium.github.io/xbee-sdk-doc/group__wpan__aps.html)
    * [Datatypes and support functions](http://exsilium.github.io/xbee-sdk-doc/group__wpan__types.html)
* [XBee Interface](http://exsilium.github.io/xbee-sdk-doc/group__xbee.html)
	* [AT Commands](http://exsilium.github.io/xbee-sdk-doc/group__xbee__atcmd.html)
    * [AT Mode](http://exsilium.github.io/xbee-sdk-doc/group__xbee__atmode.html)
    * [Device Interface](http://exsilium.github.io/xbee-sdk-doc/group__xbee__device.html)
    * [Digi Data Endpoint](http://exsilium.github.io/xbee-sdk-doc/group__xbee__digi__data.html)
		* [Over-The-Air Firmware Update Cluster](http://exsilium.github.io/xbee-sdk-doc/group__xbee__ota.html)
			* [Client](http://exsilium.github.io/xbee-sdk-doc/group__xbee__ota__client.html)
            * [Server](http://exsilium.github.io/xbee-sdk-doc/group__xbee__ota__server.html)
		* [Transparent Serial Cluster](http://exsilium.github.io/xbee-sdk-doc/group__xbee__transparent.html)
	* [Firmware Updates](http://exsilium.github.io/xbee-sdk-doc/group__xbee__firmware.html)
    * [Glue layer between XBee Device driver and WPAN](http://exsilium.github.io/xbee-sdk-doc/group__xbee__wpan.html)
    * [Node Discovery](http://exsilium.github.io/xbee-sdk-doc/group__xbee__discovery.html)
    * [Serial Interface](http://exsilium.github.io/xbee-sdk-doc/group__xbee__serial.html)
    * [XBee-specific support of ZCL Commissioning](http://exsilium.github.io/xbee-sdk-doc/group__xbee__commissioning.html)
* [Xbee_route](http://exsilium.github.io/xbee-sdk-doc/group__xbee__route.html)
* [Xbee_time](http://exsilium.github.io/xbee-sdk-doc/group__xbee__time.html)
* [ZigBee Networking](http://exsilium.github.io/xbee-sdk-doc/group__zigbee.html)
	* [ZigBee Cluster Library](http://exsilium.github.io/xbee-sdk-doc/group__zcl.html)
		* [64-bit integer support](http://exsilium.github.io/xbee-sdk-doc/group__zcl__64.html)
        * [Cluster Client support code](http://exsilium.github.io/xbee-sdk-doc/group__zcl__client.html)
        * [Clusters](http://exsilium.github.io/xbee-sdk-doc/group__zcl__clusters.html)
			* [Attribute Reporting (incomplete)](http://exsilium.github.io/xbee-sdk-doc/group__zcl__reporting.html)
            * [Basic Cluster](http://exsilium.github.io/xbee-sdk-doc/group__zcl__basic.html)
            * [Commissioning Cluster](http://exsilium.github.io/xbee-sdk-doc/group__zcl__commissioning.html)
            * [Identify Cluster](http://exsilium.github.io/xbee-sdk-doc/group__zcl__identify.html)
            * [On/Off Cluster](http://exsilium.github.io/xbee-sdk-doc/group__zcl__onoff.html)
            * [Time Cluster](http://exsilium.github.io/xbee-sdk-doc/group__zcl__time.html)
		* [Datatypes](http://exsilium.github.io/xbee-sdk-doc/group__zcl__types.html)
	* [ZigBee Data Object/ZigBee Device Profile](http://exsilium.github.io/xbee-sdk-doc/group__zdo.html)

# 2.3 Data Structures

[Data Structures](http://exsilium.github.io/xbee-sdk-doc/annotated.html)