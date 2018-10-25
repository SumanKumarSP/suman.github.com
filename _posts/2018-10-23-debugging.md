---
layout: post
title: "debugging tips"
description: "This post contains commands and approach for debugging issues on android runnning on imx6 ."
category: technical
tags: [debugging]
imagefeature: cover9.jpg

---

**ANDROID ADB COMMANDS**

### **Modem Debugging**

```
adb logcat -b radio RILJ:V '*:S'
adb logcat -b radio
adb logcat -v threadtime
adb shell dmesg
adb shell getprop gsm.version.ril-impl
```

```
ro.telephony.default_network
cat /data/system/users/0/settings_global.xml
setting id="39" name="preferred_network_mode" value="10" package="android"
```

`adb shell getprop gsm.version.ril-impl`

`adb shell getprop telephony.lteOnCdmaDevice
adb shell getprop telephony.lteOnGsmDevice`

```
** GPIO **
adb shell echo gpionum /sys/class/gpio/export
adb shell echo "out" /sys/class/gpio/gpio204/direction
adb shell echo 1 /sys/class/gpio/gpio204/active_low
adb shell echo 0 /sys/class/gpio/gpio204/value
```

---

init.config.ip

IP=$(/system/bin/getprop "dhcp.wwan0.ipaddress")
DNS1=$(/system/bin/getprop "dhcp.wwan0.dns1")
DNS2=$(/system/bin/getprop "dhcp.wwan0.dns2")
GW=$(/system/bin/getprop "dhcp.wwan0.gateway")

IFACE="wwan0"

/system/bin/ifconfig $IFACE $IP netmask 255.255.255.0 
/system/bin/route add default gw $IP dev $IFACE 
/system/bin/ip route add default via  $IP dev $IFACE 
/system/bin/ndc resolver setnetdns $IFACE $DNS1 $DNS2
/system/bin/ndc network default set $IFACE
/system/bin/ip route add default via $GW

---

### **LINUX KERNEL**

`checkpatch.pl --no-tree --terse --file filename.c`

`cat /sys/kernel/debug/gpio`

---

**DTB to DTS**

fdtdump command is part of device-tree-compiler package, install as below to get:

`sudo apt-get install device-tree-compiler`


Method-1:

`$KERNEL/scripts/dtc/dtc -I dtb -O dts -o <dts_file<dtb_file>`

Method-2:

`fdtdump <dtb_file<dts_dump>`


**DTS to DTB**

`$KERNEL/scripts/dtc/dtc -I dts -O dtb -o <dtb_file<dts_file>`

---

### **GIT**

`git remote add upstream https://github.com/boundarydevices/linux-imx6.git`


`git fetch --all`


`git cherry-pick commitid`


`git push -u origin localbranch:remotebranch`


`git branch -rvv`


`git branch -lvv`


`git blame filename`


---



{: .notice}

---