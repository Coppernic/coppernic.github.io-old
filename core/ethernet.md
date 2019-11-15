Ethernet
--------

Some devices can have Ethernet feature built-in. Ethernet is available through docking station. These devices are:

- C-One
- C-One²
- C-One e-ID
- C-One² e-ID

For C-One² and C-One² e-ID from OS Build 20190329, an option has been added to have the choice between Ethernet through docking station or Ethernet through USB
dongle. This option is called "Ethernet Cradle". It is available on device Settings. With "Ethernet Cradle" option activated, Ethernet is usable through docking
station. With "Ethernet Cradle" option disabled, Ethernet is usable through USB dongle.
When Ethernet is activated, USB port of C-One² is in Host mode. C-One² cannot be charged by USB anymore and plugging device on PC will do nothing. Device
charge is available only through docking station with AC plug connected and powered:

![](_images/settings_ethernet.png ':size=230')  ![](_images/settings_ethernet_2.png ':size=230')  ![](_images/settings_ethernet_3.png ':size=230')

### Getting started

API to enable Ethernet and "Ethernet Cradle" option is available through `EthernetConnector` class. It is available on CpcCore from version
[1.8.17](https://artifactory.coppernic.fr/artifactory/webapp/#/artifacts/browse/tree/General/libs-release-coppernic/fr/coppernic/sdk/core/CpcCore/1.8.17)

- Getting `EthernetConnector`:

```kotlin
class Net {
    private val manager = EthernetServiceManager()

    private var connector: EthernetConnector? = null

    fun getConnector() {
        manager.get().getConnector(context).subscribe({
            connector = it
        }, {
            // Handle error
        })
    }
}
```

- Enable Ethernet:

```kotlin
class Net {
    private var connector: EthernetConnector? = null

    fun enableEthernet(enable: Boolean) {
        connector?.enableEthernet(enable)
    }
}
```

- Enable Cradle:

```kotlin
class Net {
    private var connector: EthernetConnector? = null

    fun enableCradle(enable: Boolean) {
        connector?.enableCradle(enable)
    }
}
```

- Release internal resources when done:

```kotlin
class Net {
    private var connector: EthernetConnector? = null

    fun releaseResources() {
        connector?.close(enable)
    }
}
```
