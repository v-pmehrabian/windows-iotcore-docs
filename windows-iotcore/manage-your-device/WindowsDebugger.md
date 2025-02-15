---
title: Windows Debugger
author: bfjelds
ms.author: bfjelds
ms.date: 08/28/2017
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to use Windows Debugger to debug your Windows IoT Core device.
keywords: windows iot, debugger, debugging, Windows Debugger, device, tools
---

# Windows Debugger (WinDbg)
Debug your Windows 10 IoT Core device using the powerful Windows debugger, WinDbg.

The following sections describe how to successfully connect with WinDbg to a Windows 10 IoT Core device for debugging purposes.  This includes a description of the necessary software settings on the device as well as the physical hardware connections.  

WinDbg is a very powerful debugger that most Windows developers are familiar with.  However, if you are just getting started and would like to learn more about WinDbg, please visit the following links:

* [Debugging Tools for Windows](/windows-hardware/drivers/debugger/)

* [Getting Started with Windows Debugging](/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)

* [Crash Dump Analysis Using WinDbg](/windows-hardware/drivers/debugger/crash-dump-files)


## MinnowBoard Max (MBM)

You can connect WinDbg to the MinnowBoard Max device using a network connection.

### Setup network connection

In order to enable kernel debugging with WinDbg over a network, ensure that:

* An Ethernet cable is connected to MinnowBoard Max device to your network

* The MinnowBoard Max device has a valid IP address in your network

* An active connection to the MinnowBoard Max device via [PowerShell](../connect-your-device/PowerShell.md)

Using the active PowerShell connection, execute the following commands on the MinnowBoard Max to enable debugging over the network.

* `bcdedit -dbgsettings net hostip:<DEV_PC_IP_ADDRESS> port:<PORT_NUM> key:<KEY>`

	* This command enables debugging over the network.  Additionally, it specifies the IP address of the PC where WinDbg will be running (DEV_PC_IP_ADDRESS), the network port number to use for the connection (PORT_NUM), and a unique key to be used to differentiate multiple connections (KEY)

	* For PORT_NUM and KEY, you can use the following values as examples: 50045 and 1.2.3.4 respectively, although you are free to change them as you see fit

* `bcdedit -debug on`

	* This command turns on debugging on the device

* On the developer PC, start WinDbg with the PORT_NUM and the KEY values provided in the previous steps as follows:
  `"c:\Program Files (x86)\Debugging Tools for Windows (x86)\windbg.exe" -k net:port=<PORT_NUM>,key=<KEY>`

> [!NOTE]
> If you have any of the Windows kits installed, you may find WinDbg under
`C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WinDbg.exe</code>`

* Reboot the IoTCore device to reconnect to the debugger

## Raspberry Pi 2 or 3 (RPi2 or RPi3)

You can connect WinDbg to the Raspberry Pi 2 or 3 using a serial connection.

### Setup serial connection

In order to enable kernel debugging with WinDbg over a serial connection, ensure that:

* You have a debug cable such as the USB-to-TTL Serial Cable from [Adafruit](https://www.adafruit.com/product/954) or [FTDI](http://shop.clickandbuild.com/cnb/shop/ftdichip?productID=53&op=catalogue-product_info-null&prodCategoryID=105).

* An Ethernet cable or active WiFi connecting your Raspberry Pi 2 or 3 device to your network (for IP connections like SSH or PowerShell)

* The Raspberry Pi 2 or 3 device has a valid IP address in your network

* An active connection to the Raspberry Pi 2 or 3 device via [PowerShell](../connect-your-device/PowerShell.md) or [SSH](../connect-your-device/SSH.md)

UART0 will be used on the Raspberry Pi 2 or 3 device for the kernel debugging connection.  The following shows the pin mappings for the Raspberry Pi 2 or 3 as well as the serial cables:
```
        Raspberry Pi 2 or 3 pins:
            Pin #6 : GND
            Pin #8 : UART0 TX (3.3V)
            pin #10: UART0 RX (3.3V)

        Adafruit Cable:
            Black  : GND
            White  : RX  (3.3V)
            Green  : TX  (3.3V)
            Red    : PWR (5.0V NOT USED) <- DO NOT CONNECT!!

        FTDI Cable:
            Black  : GND
            Brown  : CTS (NOT USED)
            Red    : PWR (5.0V NOT USED) <- DO NOT CONNECT!!
            Orange : TX  (3.3V)
            Yellow : RX  (3.3V)
            Green  : RTS (NOT USED)
```			
The basic idea for making the correct serial connections is to remember that while one device uses its TX to transmit data, the other device uses its RX to receive the data.  Recommended connections are listed below:
```
        If using Adafruit's serial cable:
            [RPi2 or RPi3] Pin #6  (GND) <-> [Adafruti] Black (GND)
            [RPi2 or RPi3] Pin #8  (TX)  <-> [Adafruit] White (RX)
            [RPi2 or RPi3] Pin #10 (RX)  <-> [Adafruit] Green (TX)

        If using FTDI's serial cable:
            [RPi2 or RPi3] Pin #6  (GND) <-> [FTDI] Black  (GND)
            [RPi2 or RPi3] Pin #8  (TX)  <-> [FTDI] Yellow (RX)
            [RPi2 or RPi3] Pin #10 (RX)  <-> [FTDI] ORange (TX)
```
> [!NOTE]
> The EFIESP junction is no longer created. You'll have to mount it yourself,you can use mountvol command to get the GUID.
`mkdir C:\EFIESP`
`mountvol C:\EFIESP \?\Volume{ae420040-0000-0000-0000-200000000000}`

Using the active PowerShell connection, execute the following commands on the Raspberry Pi 2 or 3 device to enable debugging over the serial connection.

* `bcdedit /store c:\EFIESP\EFI\Microsoft\Boot\BCD -dbgsettings serial`

	* The above command enables the serial connection for debugging
	* The baud-rate for the Raspberry Pi 2 or 3 is hard-coded to 921600, so you don't have to specify it

* `bcdedit /store c:\EFIESP\EFI\Microsoft\Boot\BCD -debug on`

	* This command turns on debugging on the device

On the developer PC, get the COM port number PORT assigned in the system for the USB-to-TTL cable. This will be available in Device Manager under "Ports (COM & LPT)".

* `"C:\Program Files (x86)\Debugging Tools for Windows (x86)\windbg.exe" -k com:port=<PORT>,baud=921600`

	* Start WinDbg with the PORT number

> [!NOTE]
> If you have any of the Windows kits installed, you may find WinDbg under
`C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\WinDbg.exe`

* Reboot the IoTCore device to reconnect to the debugger


## DragonBoard (DB)
___

You can connect WinDbg to the DragonBoard using a serial or USB connection.

Using the active PowerShell or SSH connection to your DragonBoard, execute the following commands to enable debugging.

* `bcdedit /store c:\EFIESP\EFI\Microsoft\Boot\BCD /debug {default} ON`
	* Enables the debugger

### Setup USB connection
By default the USB debugger settings are configured in the test images.

> [!NOTE]
> Once USB kernel debugger is on, USB ports on the DragonBoard device might not work (i.e. keyboard, usb ethernet might not work).

### Setup serial connection

* `bcdedit /store c:\EFIESP\EFI\Microsoft\Boot\BCD /dbgsettings  Serial debugport:1 baudrate:115200`
	* Configures the serial port

* Reboot the IoTCore device to reconnect to the debugger