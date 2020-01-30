# MSI-GS60-2PC-GHOST-Hackintosh
MSI GS60 2 PC Laptop Hackintosh Intel HD4600 Realtek ALC 892

# Working:
- Display - Intel HD graphics with Hardware Acceleration
- Audio - Realtek ALC 892 (Laptop Speakers, Microphone and Headphones)
- Keyboard (Laptop and attached), External Mouse, Trackpad (single touch)
- USB ports as USB 2 and USB 3
- Brightness control keyboard buttons - Scroll Lock and Pause Break
- Volume control keyboard buttons - Fn+left and Fn+right arrows

# Not Working:
- Wifi and Bluetooth (alternate is using USB Wifi or Android phone US tethering via HoRNDIS)
- Nvidia Graphics Card (Laptop drivers are not available)

# Settings

# Laptop BIOS:
Note - These work for me without issues on MAC and Windows, not sure if these are best/optimized settings.
Steps - Enter BIOS via Delete key when laptop starts.

# Advanced tab:
Required to be set
- SATA Mode - AHCI
- XHCI Mode - Enabled (for USB 3)
- VT-d - Enabled (I’ve read people recommend to disable it but works fine for me as Enabled)
- Intel Virtualization Technology - Disabled

Not sure if any below impact MacOS, but mentioning as I see in my BIOS
- ERP Lot 3 - Disabled
- i-charger - Disabled
- PCI Latency - 32
- Intel SpeedStep - Enabled

# Boot Tab:
FastBoot - Disabled
Boot Mode - EFI with CSM

Boot Order priority : Hard Disk : Clover as option 3 (set Clover via using EasyUEFI; option 1,2 is USB CD/DVD and USB Hard Disk)

UEFI Hard Disk Drive Priorities : Clover as option 1 (Windows Boot Manager as 2)

# #Recommended Setup and Steps#
1. Install MacOS via VMWare or VirtualBox and download MacOS from AppStore. There are also other options to download from AppStore via Windows but I trust Virtual Machine and AppStore most.
2. Make USB installer using MACOS terminal. No Need to add boot loader.
3. Change BOOT settings as suggested.
4. Install UEFI Windows (Windows 8/8.1/10) on 1TB Hard Disk (so SSD can be exclusive for MacOS) as clean install.
5. Resize Windows partition in Disk Management and make new partition in exFat format - this format is read/write in both MacOS and Windows.
6. Use Command Prompt to mount EFI folder and Explorer++ as admin to add Clover folder inside (there should be a Microsoft folder already there).
7. Use EasyUEFI to add and move Clover entry at top of boot order.
8. In BIOS Boot tab, choose Clover as option 1 in UEFI Hard Disk priorities.
9. Confirm Clover loads and you are able to boot into Windows using Windows EFI option.
10. Format the SSD Drive Windows Partition (if present) as NTFS. Ensure if EFI folder is in SSD it is not formatted.
11. In msconfig, goto Boot option and confirm only the Hard Disk (not SSD) Windows option is present as Windows on SSD is deleted.  
12. Install MacOS on SSD using USB installer (It’ll be called Install MacOS xx) created from MacOS terminal. No Need to install Clover to USB drive as you should be able to boot from within computer.
13. After first reboot, choose boot from MacOS option (not Install MacOS xx). Vanilla MacOS installs after many boots - only first one needs to run from Install MacOS option. Do not remove USB yet.
14. Let the install complete after few reboots and once boot into MacOS is completed remove USB.
15. Enjoy!

# Further Settings post install (if AppStore or iCloud gives error) - 
1. Use Clover Configurator and navigate to SMBIOS in config.plist. Ensure internet is connected.
2. In Product Model at bottom right use dropdown and select MacBookPro11,5
3. Click check coverage. After captcha test you should get result couldn’t be found error. 
4. If valid info returns, click Generate New next to Serial Number in SMBIOS and test till you get the error. 
This ensures your random serial number is not being used by actual Mac machine and should sort out any AppStore issues.

I used Vanilla MacOS downloaded directly from AppStore. On my machine High Sierra and Mojave worked but I stuck with High Sierra due to software compatibility. I didn’t try Catalina yet and most likely won’t. All settings/modifications are only in EFI folder, no kext installed to system.

# NOTE
If you want native Wifi and Bluetooth buy an alternate Broadcom chip. No drivers for Intel wifi card.
