Core
====

Build
-----

**build.gradle**

```groovy
repositories {
        //[...]
        maven { url "https://artifactory.coppernic.fr/artifactory/libs-release" }
    }
```

```groovy
dependencies {
    implementation 'fr.coppernic.sdk.cpcutils:CpcUtilsLib:6.18.4'
    implementation 'fr.coppernic.sdk.core:CpcCore:1.8.16'

}
```

 * Last versions of libs can be found in [artifactory](https://artifactory.coppernic.fr/artifactory/webapp/#/home)
 * `implementation` is a key work of android gradle plugin 3.x.x, if you are using a older plugin, consider using `compile` instead

Hdk
---

How to use hdk on :

 * [C-One & C-One² family](core/hdk_cone.md)

Power
-----

 - [power package](core/power.md)

Others
--------

 * [Settings](core/settings.md)
 * [Key Mapping](core/mapping.md)
