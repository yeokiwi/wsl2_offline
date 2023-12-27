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
