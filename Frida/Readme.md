# Frida
An automated wrapper script for patching iOS applications (IPA files) and work on non-jailbroken device.
## Installation
- pip3 install frida-tools
- pip3 install objection
- Download Frida Server
- adb push [firda-server-xx-android-arm64] /data/local
- chmod +x [firda-server-xx-android-arm64]
- ./firda-server-xx-android-arm64

## Frida
- frida-ls-devices
- frida ps -Uai (list application ใน device ที่กำลัง connect อยู่)
- objection -g [Package name] explore
    * env
    * ios hooking list classes
    * cd [application path]
    * cd Documents
    * ios plist cat userInfo.plist
    * android sslpinning disable 

## Frida iOS Dump
- cd iOSZone\frida-ios-dump
- iproxy 2222 22
Create a new tab
- python3 dump.py [Application name]