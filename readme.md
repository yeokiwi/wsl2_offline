Use the following to install wsl2 offline

https://learn.microsoft.com/en-us/windows/wsl/install-manual

The only step that is different is:

"Once the Appx package has finished downloading, you can start running the new distribution by double-clicking the appx file. (The command wsl -l will not show that the distribution is installed until this step is complete)."
If double clicking does not work, you will need to copy the directory from c:\program file\windowapp\Canonical... to another directory

https://answers.microsoft.com/en-us/windows/forum/all/the-network-location-cannot-be-reached-for-more/8e9d94ee-2f77-4245-b4fd-debb175f46f5

There is a workaround for this problem provided by a user named Rohatsu in a GitHub discussion here is the solution
"copy contents of C:\Program Files\WindowsApps\CanonicalGroupLimited.UbuntuonWindows_1604.2017.922.0_x64__79rhkp1fndgsc to another directory (I copied to C:\Ubuntu); Windows Explorer didn't let me browse this directory so I used Total Commander (Run As Administrator) to access it and copy
start ubuntu.exe from the new location and it should install
use ubuntu.exe from the new location going forward to start up bash etc."

the discussion link
https://github.com/microsoft/WSL/issues/2577

I hope this is helpful. If you require any additional assistance, don't hesitate to respond to this.

This is a user-to-user support forum. We're users just like you helping other users to find solutions to their problems.

Best Regard
Amr

For gui display of application, use VcXSrv and follow the instructions below:
https://github.com/microsoft/WSL/issues/4793#issuecomment-577232999

installation of usbipd

https://learn.microsoft.com/en-us/windows/wsl/connect-usb

ACTIVATING USB FORWARDING TO WSL2
Purpose: make USB to Serial Bridge accessible in WSL2 to test the RPLidar SDK build on WSL Linux (Ubuntu)

Install usbipd-win on the Windows-host: https://github.com/dorssel/usbipd-win/releases

Install USBIP tools and hardware-database in Linux (WSL)
bernd@myOmen:\~$ sudo apt install linux-tools-generic hwdata
bernd@myOmen:\~$ sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*-generic/usbip 20

Open Powershell (Administrator)

PS C:\WINDOWS\system32> usbipd list
Output:
BUSID VID:PID DEVICE STATE
2-2 10c4:ea60 Silicon Labs CP210x USB to UART Bridge (COM3) Not shared
2-6 30c9:0069 HP Wide Vision HD Camera, Camera DFU Device Not shared
2-8 0461:4f03 USB Input Device Not shared
2-10 8087:0033 Intel(R) Wireless Bluetooth(R) Not shared
3-2 046d:081b Logi C310 HD WebCam Not shared
4-1 05a7:1020 Bose USB Audio, USB Input Device Not shared
4-2 046d:c52b Logitech USB Input Device, USB Input Device Not shared
4-3 04e8:329f Samsung CLP-320 Series Not shared

We're interested in sharing the CP210x, so run
PS C:\WINDOWS\system32> usbipd bind -b 2-2
where "2-2" is the value in BUSID column from usbipd list

PS C:\WINDOWS\system32> usbipd list
Output:
BUSID VID:PID DEVICE STATE
2-2 10c4:ea60 Silicon Labs CP210x USB to UART Bridge (COM3) Shared
2-6 30c9:0069 HP Wide Vision HD Camera, Camera DFU Device Not shared

"Shared" means ready to be forwarded, but still parked

PS C:\WINDOWS\system32> usbipd attach --wsl --busid 2-2 #this will now forward the USB-device. You will hear the "unplug" chime in Windows.
Output:
usbipd: info: Using WSL distribution 'Ubuntu' to attach; the device will be available in all WSL 2 distributions.
usbipd: info: Using IP address 172.26.144.1 to reach the host.

PS C:\WINDOWS\system32> usbipd list #check if it worked
Output:
BUSID VID:PID DEVICE STATE
2-2 10c4:ea60 Silicon Labs CP210x USB to UART Bridge (COM3) Attached
2-6 30c9:0069 HP Wide Vision HD Camera, Camera DFU Device Not shared

Open WSL

bernd@myOmen:~$ lsusb
Output:
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 10c4:ea60 Silicon Labs CP210x UART Bridge
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bingo!
