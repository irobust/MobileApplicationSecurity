# Mobile Application Security
รวมเอกสารและคำสั่งต่างๆ ที่ใช้สำหรับการทำ Mobile Pen-Test

## เอกสารที่เกี่ยวข้อง
* https://mas.owasp.org
* https://mas.owasp.org/MASVS/
* https://mas.owasp.org/MASTG/
* https://mas.owasp.org/checklists/
* https://cheatsheetseries.owasp.org/cheatsheets/Mobile_Application_Security_Cheat_Sheet.html

## Connect to Devices
1. Install ADB Wifi
2. Connect to Device with adb
    * adb connect [IP Address]:5555
    * adb devices -l
    * adb shell
    * adb shell pm list packages
3. Install application
    * adb install [Application Name].apk
    * adb -s emulator-5555 install helloWorld.apk
4. Upload file to device
    * adb push [local file] [remote file]
5. Download file to device
    * adb pull [local file] [remote file]
6. Backup application
    * adb backup <package name>
    * dd if=backup.ab bs=1 skip=24 | python -c "import zlib,sys;sys.stdout.write(zlib.decompress(sys.stdin.read()))" > backup.tar
7. Dump Logging
    * adb logcat -t 20
    * adb shell ps | grep -i diva (get process ID)
    * adb logcat | grep -i [Process ID]

## Diva Writeup
### Insecure Logging
- adb logcat -t 20

### Hardcoding Issues – Part 1
- jadx diva.apk
- cd diva/sources/jakhar/aseem/diva
- cat HardCodeActivity.java

### Insecure Data Storage – Part 1
- adb shell
- cd /data/data/jakhar.aseem.diva/shared_pref
- cat jakhar.aseem.diva_preferences.xml

### Insecure Data Storage – Part 2
- adb shell
- cd /data/data/jakhar.aseem.diva/databases
- sqlite3 ids2
- .tables
- select * from myuser;

Insecure Data Storage – Part 3
- cd diva/sources/jakhar/aseem/diva
- cat InsecureDataStorage3Activity.java
- adb shell
- cd /data/data/jakhar.aseem.diva
- cat uinfo...

### Input Validation Issues – Part 1
- 1' OR '1'='1'--

### Input Validation Issues – Part 2
- file:///data/data/jakhar.aseem.diva/uinfo...

### Access Control Issues – Part 1
- cd resources
- cat AndroidManifest.xml
- adb shell am start -a jakhar.aseem.diva.actions.VIEW_CREDS

### Access Control Issues – Part 2
- dz> run app.activity.start --component jakhar.aseem.diva jakhar.aseem.diva.APICreds2Activity --extra boolean check_pin false

### Access Control Issues – Part 3
- dz> run app.provider.finduri jakhar.aseem.diva
- dz> run app.provider.query content://jakhar.aseem.diva.provider.notesprovider/notes
- dz> run app.provider.query content://jakhar.aseem.diva.provider.notesprovider/notes --vertical

## Tools for Static Analysis
- Androwarn (for Android)
    * python androwarn.py -h
    * python androwarn.py -i ./SampleApplication/bin/SampleApplication.apk -r html -v 3
    * python androwarn.py -i ./SampleApplication/bin/SampleApplication.apk -d -v 3
- QARK (for Android)
    * python qarkMain.py -h
    * python qarkMain.py -p qark/sampleApp/goatdroid/goatdroid.apk   --source=1
- [MobSF](MobSF/Readme.md)
