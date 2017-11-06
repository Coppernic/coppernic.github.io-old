---
layout: post
title:  "Power Management"
date:   2017-10-23 10:14:44 +0200
categories: coppernic
---

## API from **power** package

### Prerequisites

* CpcSystemServices > 2.1.0
* CpcCore > 1.1.1

### Build

**build.gradle**
```groovy
repositories {
    mavenCentral()
    jcenter()
    maven { url 'https://artifactory.coppernic.fr/artifactory/libs-release' }
}


dependencies {
// [...]
    compile(group: 'fr.coppernic.sdk.core', name: 'CpcCore', version: '1.1.1', ext: 'aar') {
        transitive = true
    }
// [...]
}
```

### Setup

 * Create a power listener

```java
private final PowerListener powerListener = new PowerListener() {
    @Override
    public void onPowerUp(RESULT res, Peripheral peripheral) {
        if (res == RESULT.OK) {
            //Peripheral is on
        } else {
            //Peripehral power status is undefined
        }
    }

    @Override
    public void onPowerDown(RESULT res, Peripheral peripheral) {
        //Peripehral is off
    }
};
```

 * Register the listener

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    PowerManager.get().registerListener(powerListener);
}
```

 * Select a peripheral according to device and power it on

```java
if (CpcOs.isCone()) {
    peripheral = ConePeripheral.FP_IB_COLOMBO_USB;
	//Could be any other enum value corresponding to your device
} else if (CpcOs.isIdPlatform()) {
    peripheral = IdPlatformPeripheral.FINGERPRINT;
	//Could be any other enum value corresponding to your device
}

peripheral.on(context);
//The the listener will be called with the result
```

 * Power off when you are done

```java
peripheral.off(context);
//The the listener will be called with the result
```

 * release resources

```java
@Override
protected void onDestroy() {
    PowerManager.get().unregisterAll();
    PowerManager.get().releaseResources();
    super.onDestroy();
}
```

## API from **powermgmt** package (Deprecated)

### Prerequisites

* CpcSystemServices > 1.7.4
* CpcCore > x.x.x

### Build

**build.gradle**
```groovy
repositories {
    mavenCentral()
    jcenter()
    maven { url 'https://artifactory.coppernic.fr/artifactory/libs-release' }
}


dependencies {
// [...]
    compile(group: 'fr.coppernic.sdk.core', name: 'CpcCore', version: '1.1.1', ext: 'aar') {
        transitive = true
    }
// [...]
}
```

### Setup

 * Create a power utils notifier

```java
private final PowerUtilsNotifier notifier = new PowerUtilsNotifier() {
    @Override
   public void onPowerUp(RESULT res, int vid, int pid) {
        if (res == RESULT.OK) {
            //Peripheral is on
        } else {
            //Peripehral power status is undefined
        }
    }

    @Override
    public void onPowerDown(RESULT res, int vid, int pid) {
        //Peripehral is off
    }
};
```

 * Create a PowerMgmt instance

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
   PowerMgmt power = PowerMgmtFactory.get().setContext(context).setNotifier(notifier).build(); 
}
```

 * You can start using PowerMgmt object

```java
// Power finger print on
power.setPower(PeripheralTypesCone.FingerPrintReader,
               ManufacturersCone.IntegratedBiometrics,
               ModelsCone.Columbo,
               InterfacesCone.UsbGpioPort, true);
```

