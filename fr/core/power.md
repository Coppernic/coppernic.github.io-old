Power
=====

Installation
------------

* Créer un power listener:

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

 * Enregister le listener:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    PowerManager.get().registerListener(powerListener);
}
```

 * Sélectionner un périphérique en fonction de l'appareil et alimentez le:

```java
if (OsHelper.isCone()) {
    peripheral = ConePeripheral.FP_IB_COLOMBO_USB;
	//Could be any other enum value corresponding to your device
} else if (OsHelper.isIdPlatform()) {
    peripheral = IdPlatformPeripheral.FINGERPRINT;
	//Could be any other enum value corresponding to your device
}

peripheral.on(context);
//The listener will be called with the result
```

 * Eteignez le une fois fini:

```java
peripheral.off(context);
//The the listener will be called with the result
```

 * Libérez les ressources:

```java
@Override
protected void onDestroy() {
    PowerManager.get().unregisterAll();
    PowerManager.get().releaseResources();
    super.onDestroy();
}
```

Plus d'informations
-------------------

- Sur C-One, C-One² et leur version e-ID, vous pouvez utliser `MASTER_ASKEY_CONE_GPIO` pour éteindre tous les périphériques en même temps.

- Sur C-One² et C-One² e-ID, vous pouvez utiliser `USB_HOST_ASKEY_CONE_GPIO.off(context)` pour que le port USB soit mis en mode "device". Cela permet d'alimenter le C-One² par USB. Utiliser `CpcCore` à la version 1.8.16 pour cela.
