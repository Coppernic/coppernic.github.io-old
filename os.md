OS
==

All OS packages can be found on [copperpro website](https://copperpro.coppernic.fr/copperpro-downloads/).

Here below are procedures for upating OS on Coppernic’s devices.

### Prerequisites

* You shall have adb installed on your computer,
* You should be familiar with adb and how to install OS on Android platform.

C-five
------

- Copy the OS update .zip file on a SD card,
- Insert the SD card into the device,
- Press POWER & Vol. UP buttons and place the battery at the same tile,
- Hold POWER & Vol. UP buttons until getting in the Recovery menu,
- Press Vol. UP / DOWN to select “sd update” then press POWER button,
- Press Vol. UP / DOWN button to select “sd update” then press POWER button,
- Press Vol. UP / DOWN to select the correct update file,
- Press POWER button to execute the update,

- Waiting for “Install from sdcard complete” appearance,
- Press POWER button to reboot the device.
C-One
-----

- Copy the OS update .zip file on a SD card,
- Insert the SD card into the device,
- Press POWER button and select “Reset”,
- Hold P1 & Vol. UP buttons until getting in the Recovery menu,
- Press Vol. UP / DOWN button to select the correct update file,
- Press POWER button to execute the update,
- Waiting for “Install from sdcard complete” appearance,
- Press HW Reset button (under the SIM trapdoor).

ID Platform
-----------

### OTA

This method uses OTA (Over The Air) package:

* Get OTA package from [copperpro website](https://copperpro.coppernic.fr/copperpro-downloads/),
* Reboot ID Platform on Recovery mode: `adb reboot recovery`,
* On Recovery page select **adb update**,
* On your computer run `adb sideload [PACKAGE_FILE]` (Replace [PACKAGE_FILE] by the name of your package),
* When update is complete, reboot the device.

### Fastboot

If previous method fails, try this one, it uses fastboot package:

* Get fastboot package from [copperpro website](https://copperpro.coppernic.fr/copperpro-downloads/),
* Unzip package and go in unzipped folder,
* Reboot ID Platform on fastboot mode: `adb reboot fastboot`,
* On your computer, run `flash.sh` script.
    * If you are a Windows user, then feel free to update the flash script.
