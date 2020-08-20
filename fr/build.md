Build
======

Coppernic travaille avec le système de build [Gradle](https://developer.android.com/studio/build) fourni avec l'écosystème Android.
Nous ne fournissons pas de support avec les autres systèmes de build tel que Cordova, Flutter ou les anciens systèmes avec Eclipse et Ant. Nous faisons de temps en temps
une exception pour Xamarin.

Dépôt
-----

Les bibliothèques fournies par Coppernic sont stockées sur [artifactory ](https://artifactory.coppernic.fr/artifactory/webapp/#/home).

Ajouter un dépôt dans le fichier `build.gradle`

```groovy
repositories {
    //[...]
    maven { url "https://artifactory.coppernic.fr/artifactory/libs-release" }
    // Some librairies hosted on github are published in bintray
    maven { url "https://dl.bintray.com/coppernic/maven" }
}
```

Dépendances
-----------

Vous pouvez ensuite ajouter les dépendances de votre application:

```groovy
dependencies {
    // Coppernic
    implementation 'fr.coppernic.sdk.cpcutils:CpcUtilsLib:6.18.4'
    implementation 'fr.coppernic.sdk.core:CpcCore:1.8.16'

    // --- Optional

    // Ui
    implementation 'fr.coppernic.lib:splash:0.2.0'

    // Some interactors used with RxJava
    implementation 'fr.coppernic.lib:interactors:0.1.5'

    // Logging
    implementation 'com.jakewharton.timber:timber:4.7.1'
    implementation 'fr.bipi.treessence:treessence:0.3.0'
    implementation 'com.arcao:slf4j-timber:3.1'
}
```
