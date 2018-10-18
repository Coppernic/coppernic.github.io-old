---
layout: post
title:  "C-One Caen UHF"
date:   2018-07-10 11:04:44 +0200
categories: coppernic
---

C-One Caen UHF
==============

![Caen]({{"/assets/C-One_Front_01.jpeg" | absolute_url}})![Android]({{ "/assets/C-One_RFID UHF_Back.jpg" | absolute_url }})

|![Barcode]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/barcode_blue.png" }})| ![RFID]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/rfid_blue.png"}}) | ![Android]({{ "https://github.com/Coppernic/coppernic.github.io/raw/master/assets/android_blue.png"}}) |
|:---:|:---:|:---:|
|*Barcode scanning*|*RFID UHF*|*Key remapping*|

Introduction
------------

Coppernic provides a full SDK for its devices. For each specific function, developers have access to a sample application and a full documentation.

Specifications
--------------

Full Specifications for C-One can be downloaded [here](https://www.coppernic.fr/wp-content/uploads/Documentation/C-one/specification-c-one-fr.pdf).

SDK
---

Specific features for C-One Caen UHF include barcode scanning and RFID UHF reading.


### Barcode scanning

C-One is equiped with a 2D barcode scanner (Opticon MDI3100). It can read both 1D and 2D barcodes.

Documentation and sample code can be found [here](https://github.com/Coppernic/ScanSample).


### RFID UHF reading

C-One Caen UHF embeds a RFID UHF reader (Caen) especially designed for UHF applications.

For reader management, documentation and sample code can be found  [here](https://github.com/Coppernic/CaenUhfSample).


### Key remapping

C-One has 3 programmable buttons that can be managed using API. It is possible to remap a virtual key or an application.

![Android]({{ "/assets/C-One_Side_02.jpg" | absolute_url }}) ![Android]({{ "/assets/C-One_UHF_remap.png" | absolute_url }})

Documentation and source code for key remapping can be found [here](https://github.com/Coppernic/KeyRemappingSample)
