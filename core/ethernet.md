Ethernet
--------

Some devices can have Ethernet feature built-in. Ethernet is available through docking station. These devices are:

- C-One
- C-One²
- C-One e-ID
- C-One² e-ID

For C-One² and C-One² e-ID from OS Build 20190329, an option has been added to have the choice between Ethernet through docking station or Ethernet through USB
dongle. This option is called "Ethernet Cradle". 

It is available on device Settings. 
 - "Ethernet Cradle" on -> Ethernet is used through docking
 - "Ethernet Cradle" off -> Ethernet is used through USB dongle.

In both case,"Ethernet" option should be enabled to make the "Ethernet Cradle" option available.

When Ethernet is activated, USB port of C-One² is in Host mode. C-One² cannot be charged by USB anymore and plugging device on PC will do nothing. Device
charge is available only through docking station with AC plug connected and powered:

![](_images/settings_ethernet.png ':size=230')  ![](_images/settings_ethernet_2.png ':size=230')  ![](_images/settings_ethernet_3.png ':size=230')

### Getting started

API to enable Ethernet and "Ethernet Cradle" option is available through `EthernetConnector` class. It is available on CpcCore from version
[1.8.17](https://nexus.coppernic.fr/#browse/browse:libs-release:fr%2Fcoppernic%2Fsdk%2Fcore%2FCpcCore%2F1.8.17)

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

- Configure IP address: (there are no API available yet to set DHCP/ static IP)

```kotlin
class Net {
    fun congigureStaticIp() {
        StaticIpConfig.configureStatisIp(context,
                        "10.0.1.10", //IP Address
                        "24", //network prefix length
                        "10.0.0.2", //Gateway
                        "",//first DNS
                        "") //second DNS
    }
}
```
