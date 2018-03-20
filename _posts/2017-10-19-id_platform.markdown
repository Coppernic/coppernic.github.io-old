---
layout: post
title:  "ID Platform"
date:   2017-10-23 10:14:44 +0200
categories: coppernic
---

ID Platform
===========

![ID Platform]({{ "/assets/idplatform.png" | absolute_url }})

Introduction
------------

Coppernic provides a full SDK for its devices. For each specific function, developers have access to a sample application and a full documentation.

Specifications
--------------
Full specifications for ID Platform can be downloaded for [standard]({{ "/assets/Technical Specifications - ID Platform Standard.pdf" | absolute_url }}), [XS]({{ "/assets/Technical Specifications - ID Platform XS.pdf" | absolute_url }}), [XL]({{ "/assets/Technical Specifications - ID Platform XL.pdf" | absolute_url }}). 


SDK
---

### Barcode scanning

![Barcode]({{ "/assets/barcode_blue.png" | absolute_url }})

Documentation and sample code can be found here : [ScanSample](https://github.com/Coppernic/ScanSample).

### Fingerprint acquisition

![Fingerprint]({{ "/assets/fingerprint_blue.png" | absolute_url }})

Documentation and sample code can be found here : [FingerPrintSample](https://github.com/Coppernic/FingerPrintSample)

#### Suprema finger print reader

For tablets with Suprema reader, it is advised to checkout this sample instead : [SupremaSample](git@github.com:Coppernic/SupremaSample.git)

Be sure to checkout **idplatform** branch.

### RFID reading

![RFID]({{ "/assets/rfid_blue.png" | absolute_url }})

Documentation and sample code can be found here : [SeosSample](https://github.com/Coppernic/SeosSample/wiki)

### PCSC : Smart card reader

Documentation and sample code can be found here : [PcscSample](https://github.com/Coppernic/PcscSample)

OS Update
---------

All OS packages can be found on [copperpro website](https://copperpro.coppernic.fr/copperpro-downloads/#idplatform)

### Prerequisites

* You shall have adb installed on your computer. 
* You should be familiar with adb and how to install OS on Android platform


### OTA

This method uses OTA (Over The Air) package.

* Get OTA package from copperpro website
* Reboot IdPlatform on recovery mode : `adb reboot recovery`
* On recovery page, select **adb update**
* On your computer, run `adb sideload [PACKAGE_FILE]` (Replace [PACKAGE_FILE] by the name of your package)
* When update is complete, reboot device

### Fastboot

If previous method fails, try this one. It uses fastboot package.

* Get fastboot package from copperpro website
* Unzip package and go in unzipped folder
* Reboot IdPlatform on fastboot mode : `adb reboot fastboot`
* On your computer, run `flash.sh` script
    * If you are a Windows user, then feel free to update the flash script.
