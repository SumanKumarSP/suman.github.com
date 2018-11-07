---
layout: post
title: "imx6 compilation tips"
description: "This post contains tips and tricks to build individual components on imx6 android based devices."
category: technical
tags: [imx6, compilation, android]
imagefeature: cover9.jpg

---

**Android Kernel**

{% gist d92fa660476fa866761fc0bee3567fff makekernel.sh %}

---

**Sierra HLxx series RIL compilation**

{% gist 3ffcc77b8e3c4272163bbf64054c6eee sierraHL-RilCompilation %}

---

```
rm android/out/target/product/cid/obj/PACKAGING/target_files_intermediates/cid-target_files-20181008/SYSTEM/etc/apns-conf.xml

rm android/out/target/product/cid/system/etc/apns-conf.xml
```

---

**U-boot compilation**

```
cd bootable/bootloader/uboot-imx/
make cid_2g_defconfig
make all
cp u-boot.imx u-boot.cid_2g

```

---

{: .notice}

---

