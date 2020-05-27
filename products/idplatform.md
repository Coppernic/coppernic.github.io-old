ID Platform
===========

Specifications
--------------

Full specifications for ID Platform can be downloaded from [this page](https://www.coppernic.fr/en/documentations/).

Quick start
-----------

### Powering

To control powering of peripheral, `CoreServices` application needs to be installed.
This application is available on [F-Droid](fdroid.md).
Power control is done via [CpcCore](core.md) library.
More information [here](core/power.md)

### Peripherals

Each tablet can contain a set of peripherals, depending on which version you have. These peripherals can be connected to the main board via usb, serial or spi connections.

#### Permissions

[Android permissions](https://developer.android.com/guide/topics/permissions/overview) are needed to be able to communicate with usb peripherals.
These permissions removes the need to handle [USB permissions](https://developer.android.com/guide/topics/connectivity/usb/host) and to have a pop up displayed to the user.

Here is list of permissions to declare in Manifest for each peripheral family :

| Peripheral family | Permission |
| ----------------- | ---------- |
| OCR reader | `"com.id2mp.permissions.MRZ"` |
| Fingerprint reader | `"com.id2mp.permissions.FINGERPRINT"` |
| Barcode reader | `"com.id2mp.permissions.BARCODE"` |
| HID RFID reader | `"com.id2mp.permissions.HID"` |
| Smart card reader | `"com.id2mp.permissions.SCR"` |

1. Declare permission in **AndroidManifest.xml**

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="fr.coppernic.lib.interactors.ocr">

    <uses-permission android:name="com.id2mp.permissions.MRZ" />

    <application ...>
    </application>

</manifest>
```

2. [Ask for permission explicitely in your application](https://developer.android.com/training/permissions/requesting#perm-check)

[AndroidSplashScreen](https://github.com/Coppernic/AndroidSplashScreen) is here to help.

#### Samples

Samples are hosted on [gitlab](https://gitlab.com/Coppernic/idplatform/).

You need to have access granted by Coppernic team. Please ask [support](https://support.coppernic.fr/index.php) for that.
You can also send an email to [support@coppernic.fr](mailto://support@coppernic.fr)
