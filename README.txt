Problem: Growatt SPF5000ES inverter not working with USB to raspberry pi
Whats happening: Upon connecting the USB to raspberry pi, a device is detected /dev/ttyACM0 but not /dev/ttyUSB0
How to solve: Remove the cdc-acm driver and install the driver

For raspberry pi 4
==================
1. Install the kernel headers
   sudo apt-get install raspberrypi-kernel-headers
2. Compile the driver
   make
3. Remove the cdc-acm driver
   sudo rmmod cdc-acm
   sudo modprobe -r usbserial
   sudo modprobe usbserial
4. Install the driver
   sudo insmod ./xr_usb_serial_common.ko
5. Check the device
   ls /dev/ttyXRUSB*

Exar USB Serial Driver
======================
Version 1C  2017/1/11
        Add the 9-bit mode support.
        Disbale the debug messages.
Version 1B, 11/6/2015
Fixed Bug: The conditional logic to support kernel 3.9 was incorrect(line 396 in xr_usb_serial_common.c). 

Version 1A, 1/9/2015

This driver will work with any USB UART function in these Exar devices:
	XR21V1410/1412/1414
	XR21B1411
	XR21B1420/1422/1424
	XR22801/802/804

The source code has been tested on various Linux kernels from 3.6.x to 3.17.x.  
This may also work with newer kernels as well.  


Installation
------------

* Compile and install the common usb serial driver module

	# make
	# insmod ./xr_usb_serial_common.ko


* Plug the device into the USB host.  You should see up to four devices created,
  typically /dev/ttyXRUSB[0-3].


Tips for Debugging
------------------

* Check that the USB UART is detected by the system

	# lsusb

* Check that the CDC-ACM driver was not installed for the Exar USB UART

	# ls /dev/tty*

	To remove the CDC-ACM driver and install the driver:

	# rmmod cdc-acm
	# modprobe -r usbserial
	# modprobe usbserial
	# insmod ./xr_usb_serial_common.ko


Technical Support
-----------------
Send any technical questions/issues to uarttechsupport@exar.com. 

