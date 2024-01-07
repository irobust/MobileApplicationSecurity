# Networking
## Burp Suite
Installing trusted CA at the Android OS level (Root device/Emulator) for Android N+ as the following:
* `openssl x509 -inform PEM -subject_hash -in BurpCA.pem | head -1`
* `cat BurpCA.pem > 9a5ba580.0`
* `openssl x509 -inform PEM -text -in BurpCA.pem -out /dev/null >> 9a5ba580.0`
* `adb root` make sure you rooting the device
* `abd remount` set the /system writeable
* `adb push 9a5ba580.0 /system/etc/security/cacerts/`
* `adb shell “chmod 644 /system/etc/security/cacerts/9a5ba580.0”`
* `adb shell “reboot”`
* Check Settings > Security > Trusted Credentials > SYSTEM to confirm your newly added CA is listed.

## Wireshark
Live packet capture in realtime
* adb shell "tcpdump -s 0 -w - | nc -l -p 4444"
* adb forward tcp:4444 tcp:4444
* nc localhost 4444 | sudo wireshark -k -S -i –
