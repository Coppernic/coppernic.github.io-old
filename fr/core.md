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

 * Les dernières versions de libs sont disponible sur [artifactory](https://artifactory.coppernic.fr/artifactory/webapp/#/home).
 * `implementation` est un mot clé du plugin Gradle 3.x.x pour Android, si vous utilisez un plugin plus ancien, utilisez `compile` à la place.

HDK
---

Comment utiliser HDK sur:

 * [Famille des C-One & C-One²](/fr/core/hdk_cone.md)

Power
-----

 - [Alimentation](/fr/core/power.md)

Autres
------

 * [Paramètres](/fr/core/settings.md)
 * [Mappage des touches](/fr/core/mapping.md)
