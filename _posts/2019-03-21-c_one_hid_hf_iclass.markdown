---
layout: post
title:  "C-One² HID HF iClass"
date:   2019-03-21 10:14:44 +0200
categories: coppernic
---

C-One² HID HF iClass
============

![HID HF]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/C-One_Front_01.jpeg"}})


|![Barcode]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/barcode_blue.png" }})| ![RFID]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/rfid_blue.png"}}) | ![Android]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/android_blue.png"}}) |
|:---:|:---:|:---:|
|*Barcode scanning*|*RFID HF/LF*|*Key remapping*|

Introduction
------------

Coppernic provides a full SDK for its devices. For each specific function, developers have access to a sample application and a full documentation.

Specifications
--------------

Full Specifications for C-One² can be downloaded [here](https://www.coppernic.fr/wp-content/uploads/Documentation/C-one/specification-c-one-fr.pdf).

SDK
---

Specific features for C-One² HID HF iClass include barcode scanning and RFID HF reading.


### Barcode scanning

C-One² is equiped with a 2D barcode scanner. It can read both 1D and 2D barcodes.

Documentation and sample code can be found [here](https://github.com/Coppernic/ScanSample).


### RFID HF/LF reading

C-One² HID iClass embeds a RFID HF/LF reader.

The library and javadoc for CpcHidIclass can be found [here](https://artifactory.coppernic.fr/artifactory/webapp/#/artifacts/browse/tree/General/libs-release/fr/coppernic/sdk/hid/iclassProx/CpcHidIClassProx).

For basic reader management, documentation and sample code can be found [here](https://github.com/Coppernic/HidIclassSample).


### Key remapping

C-One² has 3 programmable buttons that can be managed using API. It is possible to remap a virtual key or an application.

![Android]({{ "/assets/C-One_Side_01.jpg" | absolute_url }}) ![Android]({{ "/assets/C-One_Side_02.jpg" | absolute_url }})

Documentation and source code for key remapping can be found [here](https://github.com/Coppernic/KeyRemappingSample)
