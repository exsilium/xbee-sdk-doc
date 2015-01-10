<h1>9. Troubleshooting</h1>

* When attempting to debug an application I receive the following error and I cannot continue with the process:
![Debugger not found](doc/images/img011c.jpg)
	* CodeWarrior <script type="text/javascript">acronym("IDE")</script><acronym title="Integrated Development Environment">IDE</acronym> could not find your debugger. Make sure it is properly connected to any <script type="text/javascript">acronym("USB")</script><acronym title="Universal Serial Bus">USB</acronym> port of your <script type="text/javascript">acronym("PC")</script><acronym title="Personal Computer">PC</acronym>.
	* Try to connect the debugger to a different <script type="text/javascript">acronym("USB")</script><acronym title="Universal Serial Bus">USB</acronym> port of your <script type="text/javascript">acronym("PC")</script><acronym title="Personal Computer">PC</acronym>.

* When trying to debug/launch an application I receive the following error and the process doesn't continue:
![Reset needed](doc/images/img011d.jpg)
	* Try to power-off and power-on the <script type="text/javascript">acronym("XBIB")</script><acronym title="XBee Interface Board">XBIB</acronym> device so that CodeWarrior will try to enter in debug mode with the XBee module through a power on reset sequence.

* I'm having problems to running some WPAN examples, the projects are built	and launched correctly but they don't work.
	* Most of the WPAN examples need an XBee network in order to operate. In the majority of cases, this network is started by the X-Stick that comes with the kit. So verify the following:
		* Ensure that the X-Stick is connected to one of the <script type="text/javascript">acronym("USB")</script><acronym title="Universal Serial Bus">USB</acronym> ports of your <script type="text/javascript">acronym("PC")</script><acronym title="Personal Computer">PC</acronym>.
		* It is possible that your XBee modules have joined a different XBee network started by other devices. Make sure the XBee module has the same PAN ID as the X-Stick so that the XBee module will join the network started by the X-Stick. Refer to topic [10.10. Configuring an XBee network](tips_tricks.md#1010-configuring-an-xbee-network) for more information.

* When I try to open the config.xml file of a project, I receive the following error in the editor instead of the contents of my project:
![Editor error](doc/images/img011e.jpg)
	* The most probable cause of this error is that your XBee application project does not have an XBee firmware library configured, or it is using a library that does not exist.
> You can try to fix the problem by refreshing the sources of your project. See topic [10.8. Refreshing the project sources](tips_tricks.md#108-refreshing-the-project-sources) for more information.

* When I try to open a configuration file (config.xml) located outside of the workspace, I receive the following error:
![Editor error external](doc/images/img011f.jpg)
	* In order to display the contents of a configuration file, the file needs to be contained within a project in the workspace. The reason being that the <script type="text/javascript">acronym("IDE")</script><acronym title="Integrated Development Environment">IDE</acronym> needs to access the settings of the project to know which templates should be used to display the components of the file.
> Therefore, it is not possible to display the components of an external config.xml file.

* The application I flashed in my XBee module does not start automatically after a power reset.
	* Your XBee module may be missing the bootloader, or part of the bootloader could be erased. See topic [5. Flashing a debuggable bootloader](flashing_bootloader.md) for information about how to flash a bootloader in your XBee module.
> Please note that you will have to flash your application again after flashing the bootloader.

* Applications for the 128KB family of XBee modules do not work or have stopped working.
	* Your XBee module may be missing the bootloader, or part of the bootloader could be erased. See topic [5. Flashing a debuggable bootloader](flashing_bootloader.md) for information about how to flash a bootloader in your XBee module.
> Please note that you will have to flash your application again after flashing the bootloader.

> The most common cause of this problem is that you have tried to flash an XBee application project built for a 32KB module into a 128KB one. This process erases part of the bootloader of the 128KB module and applications will stop working.
