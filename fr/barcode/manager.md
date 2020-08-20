Barcode Manager
==============

> Pour C-One et C-five :
> Ancienne documentation [ici](https://github.com/Coppernic/ScanSample/blob/1.0.0/README.md)

API pour utiliser le scanner de codes à barres via le service Barcode Manager.

Il y a 2 manières de déclencher la lecture d'un code à barres:

 - affecter un bouton physique à la fonction scan de code barre.
 - envoyer un *Intent*

## Terminaux compatibles

- C-One² et C-One² e-ID
- IDPlatform

Cette API est presque la même que l'ancienne. Les principales différences sont :
- pour les appareils *C-One* and *C-five*,`barcode service` est contenu dans
 l'application `CpcSystemServices`. Pour la famille des *C-One²* et
 *ID Platform*, `barcode service` est contenu dans l'application `Barcode Manager`.
 - l'`applicationId` est différent pour ces applications donc les `Intents` utilisés pour contrôler le lecteur de code barres ont un `ComponentName` différents.

Par exemple, sur *C-One²* nous utilisons `Intent.setPackage()` de cette façon :

```java
intent.setPackage(OsHelper.getSystemServicePackage(context, "fr.coppernic.features.barcode"));
```

sur *C-five*, nous utlisons `Intent.setPackage()` de cette façon :

```java
intent.setPackage(OsHelper.getSystemServicePackage(context));
```

## Associer un bouton physique à la lecture de code barres

Dans l'application de paramètres d'Android, aller à <kbd>remap key & shortcuts</kbd> (peut changer selon les appareils), et associer un bouton à <kbd>SCAN</kbd> ou <kbd>Barcode Scan</kbd> (en fonction du terminal).

## Intents

Ce service répond aux `Intents`. Il y a 2 façons de communiquer via `Intents`:

- ajouter une dépendance à la librairie CpcBarcode et utiliser ses fonctions *Helper*
- développer un `Intent` from scratch et l'utiliser

Dans tous les cas, vous devrez déclarer une permission pour être capable de communiquer avec le service.

- **Permissions**

Vous devez déclarer la permission `fr.coppernic.permission.BARCODE` dans votre manifest:

```xml
    <uses-permission android:name="fr.coppernic.permission.BARCODE" />
```

Et vous devez également explicitement demander cette permission:

```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
    requestPermissions(new String[]{"fr.coppernic.permission.BARCODE"}, 42)
}
```

### Intents via CpcBarcode

- **Ajout de la dépendance CpcBarcode**

Plus d'informations [ici](https://developer.coppernic.fr/#/barcode/library)

- **Démarrer le service**

```java
ComponentName cn = BarcodeReader.ServiceManager.startService(context);
if(cn == null) {
    // Error
}
```

- **Arrêter le service**

```java
ComponentName cn = BarcodeReader.ServiceManager.stopService(context);
if(cn == null) {
    // Error
}
```

- **Déclencher un scan**

```java
ComponentName cn = BarcodeReader.ServiceManager.startScan(context);
if(cn == null) {
    // Error
}
```

- **Arrêter un scan**

```java
ComponentName cn = BarcodeReader.ServiceManager.stopScan(context);
if(cn == null) {
    // Error
}
```

### Intents avec CpcCore

#### Démarrer le service

```java
import fr.coppernic.sdk.core.Defines;
import fr.coppernic.sdk.utils.helpers.OsHelper;

public void startScan(){
    Intent scanIntent = new Intent();
    // Set package target for intent. We are using OsHelper to get real package name according to the device we are running on
    scanIntent.setPackage(OsHelper.getSystemServicePackage(context, "fr.coppernic.features.barcode"));
    // Set action for scan trig
    scanIntent.setAction("fr.coppernic.intent.action.start.barcode.service");
    // Tell service who we are
    scanIntent.putExtra(Defines.Keys.KEY_PACKAGE, context.getPackageName());
    // Send intent to service
    ComponentName ret;
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        ret = context.startForegroundService(intent);
    } else {
        ret = context.startService(intent);
    }
}
```

#### Arrêter le service

```java
import fr.coppernic.sdk.core.Defines;
import fr.coppernic.sdk.utils.helpers.OsHelper;

public void startScan(){
    Intent scanIntent = new Intent();
    // Set package target for intent. We are using OsHelper to get real package name according to the device we are running on
    scanIntent.setPackage(OsHelper.getSystemServicePackage(context, "fr.coppernic.features.barcode"));
    // Set action for scan trig
    scanIntent.setAction("fr.coppernic.intent.action.stop.barcode.service");
    // Tell service who we are
    scanIntent.putExtra(Defines.Keys.KEY_PACKAGE, context.getPackageName());
    // Send intent to service
    ComponentName ret;
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        ret = context.startForegroundService(intent);
    } else {
        ret = context.startService(intent);
    }
}
```

#### Déclencher un scan

```java
import fr.coppernic.sdk.core.Defines;
import fr.coppernic.sdk.utils.helpers.OsHelper;

public void startScan(){
    Intent scanIntent = new Intent();
    // Set package target for intent. We are using OsHelper to get real package name according to the device we are running on
    scanIntent.setPackage(OsHelper.getSystemServicePackage(context, "fr.coppernic.features.barcode"));
    // Set action for scan trig
    scanIntent.setAction(Defines.IntentDefines.INTENT_ACTION_SCAN);
    // Tell service who we are
    scanIntent.putExtra(Defines.Keys.KEY_PACKAGE, context.getPackageName());
    // Send intent to service
    ComponentName ret;
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        ret = context.startForegroundService(intent);
    } else {
        ret = context.startService(intent);
    }
}
```

Quand le lecteur est en lecture continue, il doit être arrêté de façon explicite, **même si un code barres est lu**. Autrement, il est arrêté automatiquement par une lecture ou un timeout.

#### Arrêter un scan

Arrêter un scan est requis quand le lecteur est en lecture continue.

```java
import fr.coppernic.sdk.core.Defines;
import fr.coppernic.sdk.utils.helpers.OsHelper;

public void stopScan(){
    Intent scanIntent = new Intent();
    // Set package target for intent. We are using OsHelper to get real package name according to the device we are running on
    scanIntent.setPackage(OsHelper.getSystemServicePackage(context, "fr.coppernic.features.barcode"));
    // Set action for scan trig
    scanIntent.setAction(Defines.IntentDefines.INTENT_ACTION_STOP_SCAN);
    // Tell service who we are
    scanIntent.putExtra(Defines.Keys.KEY_PACKAGE, context.getPackageName());
    // Send intent to service
    ComponentName ret;
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        ret = context.startForegroundService(intent);
    } else {
        ret = context.startService(intent);
    }
}
```

### Récupérer le résultat d'un scan

 - Enregistrer un broadcast receiver

```java
import fr.coppernic.sdk.core.Defines;

public class Example extends android.app.Activity {
    private void registerReceiver() {
        IntentFilter filter = new IntentFilter();
        filter.addAction(Defines.IntentDefines.ACTION_SCAN_SUCCESS);
        filter.addAction(Defines.IntentDefines.ACTION_SCAN_ERROR);
        registerReceiver(scanResult, filter);
    }

    @Override
    protected void onResume() {
        super.onResume();
        registerReceiver();
    }

    @Override
    protected void onPause() {
         super.onPause();
         unregisterReceiver(scanResult);
    }
}
```

 - Récupérer le résultat


```java
import fr.coppernic.sdk.core.Defines;
import fr.coppernic.sdk.utils.core.CpcResult.RESULT;

public class Example extends android.app.Activity {
    private final BroadcastReceiver scanResult = new BroadcastReceiver() {
        @Override
        public void onReceive(Context context, Intent intent) {
            Log.d(TAG, "Receive " + intent + ", " + ObjPrinter.bundleToString(intent.getExtras()));
            if (intent.getAction().equals(ACTION_SCAN_SUCCESS)) {
                String dataRead = intent.getExtras().getString(BARCODE_DATA);
            } else if (intent.getAction().equals(ACTION_SCAN_ERROR)) {
                int result = intent.getIntExtra(KEY_RESULT, CpcResult.RESULT.ERROR.ordinal());
                CpcResult.RESULT resultAsEnum = CpcResult.RESULT.values()[result];
                Toast.makeText(context, getString(R.string.scan_error, resultAsEnum.toString()), Toast.LENGTH_SHORT).show();
            }
        }
    };
}
```

Les extras des Intents sont :
 - **Defines.Keys.KEY_RESULT**: `int`, résultat du scan. Vous pouvez utiliser `CpcResult.getResultFromOrdinal(int)` pour avoir un `RESULT`
 - **Defines.Keys.KEY_BARCODE_DATA**: `String`, les données scannées. Disponibles uniquement quand le résultat est `RESULT.OK`
 - **Defines.Keys.KEY_BARCODE_DATA_BYTES**: `byte[]`, les données scannées en tableau de bytes. Disponibles uniquement quand le résultat est `RESULT.OK`

### Defines

  - **Defines.IntentDefines.INTENT_ACTION_SCAN** : `"fr.coppernic.intent.action.SCAN"`
  - **Defines.IntentDefines.INTENT_ACTION_STOP_SCAN** : `"fr.coppernic.intent.action.scan.STOP"`
  - **Defines.IntentDefines.ACTION_SCAN_SUCCESS** : `"fr.coppernic.intent.scansuccess"`
  - **Defines.IntentDefines.ACTION_SCAN_ERROR** : `"fr.coppernic.intent.scanfailed"`
  - **Defines.Keys.KEY_PACKAGE** : `"package"`
  - **Defines.Keys.KEY_RESULT** : `"res"`
  - **Defines.Keys.KEY_BARCODE_DATA** : `"BarcodeData"`
  - **Defines.Keys.KEY_BARCODE_DATA_BYTES** : `"BarcodeDataBytes"`
  - Package
     - C-One² Android 7 : `"fr.coppernic.features.barcode.conen"`
     - C-One² Android 8 : `"fr.coppernic.features.barcode.coneo"`
     - IDPlatform : `"fr.coppernic.features.barcode.idplatform"`
     - ...

## Configurer le service de code barres

Le lecteur de code barres peut être configuré via l'application **Barcode Manager**. Cette application est habituellement installée sur les terminaux.
Elle est également disponible sur [CopperApps](/fr/copperapps).

#### Général

* **Scan sound** : joue un son avec une lecture réussie ou non
* **Scan display** : affiche/cache un indicateur de scan à l'écran (Régler cette option à `false` sauf si vous savez ce que vous faites)
* **Continuous mode** : active/désactive la lecture continue (scan jusqu'à ce que le bouton soit relâché ou qu'un code barre soit lu)
* **Scan timeout** : délai de scan
* **Barcode service startup at boot** : active/désactive le démarre automatique du service Barcode quand l'appareil a fini de démarrer.
* **Keep barcode reader opened**: si sélectionné, améliore la vitesse de lecture
* **Keyboard wedge**: envoie les données au tampon d'entrée en plus de l'intent
* **Keyboard fast wedge**: utilise un keyboard wedge plus rapide, une application clavier supplémentaire doit être installée
* **Search and replace**: utilise une expression régulière pour chercher un pattern dans les données et les remplacer par une autre valeur

#### Lecteur de code à barres

Paramètres spécifique au lecteur de code à barre.

#### Paramètres

Dépend de l'appareil.

#### Symbologies

Permet à l'utilisateur d'activer/désactiver des symbologies, d'ajouter des suffixes et préfixes, d'ajouter une taille minimale et maximale à ce qui peut être lu.

### Utiliser la librairie CpcBarcode

Pour configurer le service, vous devez utiliser **CpcBarcode** disponible dans le SDK.

```java
import fr.coppernic.lib.barcode.core.GlobalConfig;

public class Example {
    public void configure(){
        // GlobalConfig is the class that will configure the barcode service.
        final GlobalConfig globalConfig = GlobalConfig.Builder.get(context);
        //enable or disable sound during scan
        globalConfig.enableSound(enable);
        //set continuous mode
        globalConfig.enableContinuous(enable);
        //set scan timeout (used when continuous mode is disabled
        globalConfig.setScanTimeoutSoft(timeout);
        //enable service notification
        globalConfig.enableDisplayStartupNotif(enable);
        //Enable service launch at device's startup
        globalConfig.enableBarcodeServiceStartAtBoot(enable)
    }
}
```
