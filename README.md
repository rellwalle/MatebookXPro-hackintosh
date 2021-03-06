# Matebook X Pro Hackintosh
This is the guide to install macOS onto the Huawei Matebook X Pro.

### Feel free to help a broke student out at the bottom of the page. :)

[English](README.md) | [中文](README-CN.md)| [Español](README-ESP.md)

***DISCLAIMER***
The project is still in its beta/testing state.
Proceed at your own risk, I shall not take responsibility for any damages caused.

## My Matebook X Pro's Hardware Configuration:
- CPU: i7-8550U @ 1.8GHz
- 16GB RAM
- Nvidia GTX MX 150 / Intel UHD 620
- 3K display @ 3000x2000
- 512 Gb Toshiba SSD (Not tested on Liteon SSDs yet)
- USB Wifi: Edimax N150

## What works:
- Intel UHD 620 Graphics Acceleration (we are using a CoffeeLake platform-id for now, will try to 	switch to native Kabylake graphics)
- Realtek alc256 Audio via VoodooHDA (please help generate a custom AppleHda layout if you want to 	help, right now all existing layouts makes the tweeters work)
- Keyboard with Volume Controls (via VoodooPS2)
- HDMI + Thunderbolt 3 (TB3 at least works as a display output, not sure about other functionality)
- Camera support up to 10.14.0
- Trackpad and Native Gestures via VoodooI2c (Four fingers support is not well implemented, please 	try using five fingers as a substitution)
- Touchscreen with multi-touch capabilities (think of it as a large trackpad)
- Battery Percentage (via ACPIBatteryManager)
- Bluetooth (Not stable, further examination is required)
- Power Management (via CPUFriend and CPUFriendProvider, CPU idles at 1.2Ghz though Windows idles 	at 0.8Ghz, needs improvement)(kext taken from TheDarkVoid's Dell XPS 9360 guide)
- Wifi via USB dongle

## What doesn't Work:
- Brightness and Sleep (Likely due to spoofing Coffeelake Graphics)
- dGPU (Nvidia Optimus not supported on MacOS)
- eGPU (not tested)
- Fingerprint Sensor
- Intel Wifi (soldered onto the motherbaord)

## Let's Get Started

### What you need:
- Huawei Matebook X Pro (either i7 or i5 model, though i5 model has not been tested)
- macOS or OS X downloaded from the Mac App Store
- 8GB USB stick
- External USB Wifi Dongle
- USB C dock (for connecting to external mouse for initial setup)

### BIOS Settings
- f2 is for booting into BIOS
- f12 is for boot override
- Any version of the BIOS is good, but I'm version 1.18
- Restore Defaults
- Disable Secure boot
- Matebook's BIOS is rewrite protected, EFI tool is useless against this BIOS.

## Pre-Install:
Prior to installing macOS, it is a good idea to backup any important files on Windows.

You can also leave Windows intact, but it can get tricky. Read here for more information: 
http://www.tonymacx86.com/multi-booting/133940-mavericks-windows-8-same-drive-without-erasing.html

This guide for creating USB and installing using Clover UEFI works well for this laptop: 
https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/

For the installation purposes, please use the HD620 plist that rehabman provides in his guide for your installation USB.

***Set config.plist/Graphics/ig-platform-id=0x12345678 for installation.***

I ended up wiping windows and installing it afterwards, if you do so, fingerprint sensor will stop working, please follow the guide from this link:
http://bradshacks.com/matebook-x-pro-fingerprint/

Install macOS according to post 2 of the guide:
https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/

Post Installation

You should now be at your desktop.

Download
- Clover Configurator Pro
	https://github.com/Micky1979/Clover-Configurator-Pro/blob/master/Updates/CCP_v1.4.1.zip?raw=true
- USB Wi-fi Drivers
- Newest Clover Bootloader, and install it to your boot disk
	https://sourceforge.net/projects/cloverefiboot/

Mount EFI partition if not mounted already

Clone the repository via terminal or download it and swap the CLOVER folder downloaded for the one in your EFI directory.

***Note if you have the i5 version, or any other configurations of the laptop sold exclusively in China***, you should:
- delete the DSDT.aml file in /Volumes/EFI/EFI/CLOVER/ACPI/patched and generate your own via pressing f4 	at the clover bootscreen.
- For i5 models: you have to make a custom CPUFriendProvider for Power Management by following this 		guide:
	https://github.com/PMheart/CPUFriend/blob/master/Instructions.md

Reboot

You should have a half functioning Matebook X Pro Hackintosh by now. 

Known Problems and Partial Solutions:
- Brightness not working: download brightness slider from the App Store, it doesn't change the actual 		brightness, but it pleases the eye since it changes the white spot level or something along 		those lines.
	https://itunes.apple.com/us/app/brightness-slider/id456624497?mt=12
- Sleep doesn't work: after waking from a sleep (closing the lid), your computer will wake and you will 	see a graphics glitch. This should be due to Coffeelake spoofing. We are trying to fix this. 
- Bluetooth: you will need a copy of 10.13.6's IOBluetoothFamily.kext and install it to S/L/E via 		kextbeast.

### Credits:
- Darren_Pan on reddit
- midi and Maemo on discord
- Chinese Matebook X Pro Hackintosh community
- Spanish Matebook X Pro Hackintosh community
- All the developers who developed the kexts used in this guide.

### Help a broke student out:
- PayPal:
	https://www.paypal.me/gnodipac886#%20MatebookXPro-hackintosh
- Venmo:
	https://venmo.com/code?user_id=2386577070227456090
	
QR Codes:

| PayPal                                                     | Venmo.                                                     | WeChat                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------- |
| ![PayPal_160]( https://github.com/gnodipac886/MatebookXPro-hackintosh/blob/master/Help%20a%20Broke%20Student%20out/paypal.png?raw=true) | ![venmo_160](https://github.com/gnodipac886/MatebookXPro-hackintosh/blob/master/Help%20a%20Broke%20Student%20out/venmo.jpg?raw=true) | ![Wechat_160](https://github.com/gnodipac886/MatebookXPro-hackintosh/blob/master/Help%20a%20Broke%20Student%20out/WeChat.jpg) |

Good Luck!
