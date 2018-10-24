---
layout: post
title: "imx6 compilation tips"
description: "This post contains tips and tricks to build individual components on imx6 android based devices."
category: technical
tags: [imx6, compilation, android]
imagefeature: cover9.jpg

---

**ANDROID KERNEL**

> makekernel.sh
> 
> #!/bin/sh
> 
> cd out/target/product/cid
> 
> rm boot.img
> 
> rm boot/zImage
> 
> rm ./boot/imx6q-cid.dtb ./boot/imx6q-cid2.dtb
> 
> cd -
> 
> cd kernel_imx
> 
> mv tags ../
> 
> rm .config
> 
> make distclean
> 
> cd -
> 
> mv tags kernel_imx/
> 
> make -j16 bootimage

<script src="https://gist.github.com/SumanKumarSP/d92fa660476fa866761fc0bee3567fff.js"></script>

{% gist d92fa660476fa866761fc0bee3567fff makekernel.sh %}

---

**Sierra HLxx series RIL compilation**

rm -rf android/out/target/product/cid/obj/NOTICE_FILES/src/system/lib/libsierrahl-ril.so.txt

rm -rf android/out/target/product/cid/obj/PACKAGING/target_files_intermediates/cid-target_files-20181008/SYSTEM/lib/libsierrahl-ril.so

rm -rf android/out/target/product/cid/obj/SHARED_LIBRARIES/libsierrahl-ril_intermediates/LINKED/libsierrahl-ril.so

rm -rf android/out/target/product/cid/obj/SHARED_LIBRARIES/libsierrahl-ril_intermediates/PACKED/libsierrahl-ril.so

rm -rf android/out/target/product/cid/obj/lib/libsierrahl-ril.so

rm -rf android/out/target/product/cid/symbols/system/lib/libsierrahl-ril.so

rm -rf android/out/target/product/cid/system/lib/libsierrahl-ril.so

rm android/out/target/product/cid/obj/PACKAGING/target_files_intermediates/cid-target_files-20181008/SYSTEM/etc/apns-conf.xml

rm android/out/target/product/cid/system/etc/apns-conf.xml

mmm hardware/sierra/

make -j16

---

**U-boot compilation**

cd bootable/bootloader/uboot-imx/

make cid_2g_defconfig

make all

cp u-boot.imx u-boot.cid_2g

---

**DTB to DTS**

> fdtdump command is part of device-tree-compiler package, install as below to get:
>
> `sudo apt-get install device-tree-compiler`


Method-1:

`$KERNEL/scripts/dtc/dtc -I dtb -O dts -o <dts_file> <dtb_file>`

Method-2:

`fdtdump <dtb_file> > <dts_dump>`


**DTS to DTB**

`$KERNEL/scripts/dtc/dtc -I dts -O dtb -o <dtb_file> <dts_file>`

---


{: .notice}

---

