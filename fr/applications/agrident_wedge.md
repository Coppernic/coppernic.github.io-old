Agrident Wedge
=====


Introduction
------------
Cette application explique comment utiliser l'application Agrident Wedge sur un C-One² disposant d'un lecteur RFID LF Agrident.
L'application est composée de deux parties:

 - Agrident Wedge Settings (AW Settings)
 - Agrident Wedge Scan (AW Scan)


Prérequis
---------

### C-One² LF Agrident

 - CoreServices version 1.9.0 et supérieure doit être installée sur le terminal.
 - Agrident Wedge 2.2.0 et supérieure doit être installée sur le terminal.

 Les application sont disponibles sur [CopperApps](copperapps.md) (Disponible en téléchargement [ici](https://coppernic.fr/copperapps.apk)).

Qu'est ce qu'un keyboard wedge?
-------------------------------

Une application keyboard wedge est une application qui récupère des données du lecteur et qui les envoie directement dans la zone tampon du clavier, comme si elles avaient été tapées sur un clavier virtuel. Elles sont ensuite insérées automatiquement dans les champs de texte par le système Android.

Les applications Coppernic de type wedge offrent une meilleure intégration grâce à l'utilisation d'`Intent` Android en plus des données insérées dans le buffer du clavier. On peut ainsi savoir si la lecture a réussie ou non, récupérer le code d'erreur ou tout simplement récupérer les données du lecteur de manière beaucoup plus réactive. Ces données peuvent être traité par l'application avant affichage à l'opérateur.


Paramètres Agrident
-------------------

Les paramètres de l'application *Agrident Wedge* permettent la configuration du son, des délais, et bien d'autres...


![](_images/agrident_settings.png)

 - Scan Sound: joue un son après une lecture réussie ou non.
 - Scan Display: affiche une icône durant la lecture.
 - Scan Timeout: configure la durée pendant laquelle le lecteur va essayer de lire un tag.
 - Agrident Service startup boot: si activé, le service va se lancer automatiquement au démarrage du terminal.
 - Continuous Read: le lecteur va lire en permanence jusqu'à ce que le service soit stoppé ou l'écran éteint.
 - Keyboard Wedge: si activé, envoie le résultat au clavier. Un `Intent` est toujours envoyé.
 - Scan Enter: ajoute un retour chariot dans le tampon du clavier après les données lues.
 - Remove leading 0: supprime le caractère `0` au début des données envoyées.

 Agrident Wedge Scan
 ---------------------

 Cette application lance un scan pour lire un tag LF.
 Vous pouvez utiliser cette application en l'associant avec un (ou plusieurs) bouton programmable. Vous pouvez effectuer cette opération sur le terminal dans `Paramètres` -> `Remap key & shorcut`.


 Utiliser Agrident Wedge comme un clavier
 ----------------------------------------

 - Associer l'application *Agrident Wedge Scan* avec un (ou plusieurs) bouton programmable du C-One.
 - Configurer l'option *Keyboard Wedge* de l'application
 - Appuyer sur le bouton.
 - Les données sont envoyées au système comme des entrées clavier.


 Utiliser Agrident Wedge avec des Intents.
 -----------------------------------------

 - Pour cet exemple, la librairie utilitaire de Coppernic est utilisée. Vous devez la déclarer dans votre build.gradle:

 ``` groovy
 // Au niveau du projet
 allprojects {
     repositories {
         google()
         jcenter()
         maven { url "https://artifactory.coppernic.fr/artifactory/libs-release" }
     }
 }
 ```

 ``` groovy
 // Au niveau du module
 dependencies {
     implementation 'fr.coppernic.sdk.cpcutils:CpcUtilsLib:6.13.0'
}
 ```


 - Déclarer un `BroadcastReceiver` dans votre classe, il recevra les intents en provenance de l'application *Agrident Wedge*.

 ``` java
 private BroadcastReceiver agridentReceiver = new BroadcastReceiver() {
     @Override
     public void onReceive(Context context, Intent intent) {        
         if (intent.getAction().equals(CpcDefinitions.ACTION_AGRIDENT_SUCCESS)) {
             // Data is available as a String
             String dataRead = intent.getStringExtra(CpcDefinitions.KEY_BARCODE_DATA);           
         } else if (intent.getAction().equals(CpcDefinitions.ACTION_AGRIDENT_ERROR)) {
             // Read failed (main cause is timeout)
         }
     }
 };
 ```

 - Enregister le receiver, par exemple dans la méthode `onStart()`

 ``` java
 @Override
 protected void onStart() {
     super.onStart();
     // Registers agrident wedge intent receiver
     IntentFilter intentFilter = new IntentFilter();
     intentFilter.addAction(CpcDefinitions.ACTION_AGRIDENT_SUCCESS);
     intentFilter.addAction(CpcDefinitions.ACTION_AGRIDENT_ERROR);
     registerReceiver(agridentReceiver, intentFilter);
 }
 ```

 - Et désinscrivez le, dans la méthode `onStop()` par exemple:

 ``` java
 @Override
 protected void onStop() {
     // Unregisters agrident wedge receiver
     unregisterReceiver(agridentReceiver);
     super.onStop();
 }
 ```

 - Déclencher une lecture:

 ```java
 private static final String AGRIDENT_WEDGE = "fr.coppernic.tools.cpcagridentwedge";

 // Starts Agrident wedge
 Intent launchIntent = getPackageManager().getLaunchIntentForPackage(AGRIDENT_WEDGE);
 if (launchIntent != null) {
     startActivity(launchIntent);//null pointer check in case package name was not found
 }
 ```

 Si vous ne voulez pas déclarer CpcUtilsLib dans votre application, voici les valeurs des constantes:

 ```java
 public static final String ACTION_AGRIDENT_SUCCESS = "fr.coppernic.intent.agridentsuccess";
 public static final String ACTION_AGRIDENT_ERROR = "fr.coppernic.intent.agridentfailed";
 public static final String ACTION_AGRIDENT_SERVICE_STOP = "fr.coppernic.intent.action.stop.agrident.service";
 public static final String ACTION_AGRIDENT_SERVICE_START = "fr.coppernic.intent.action.start.agrident.service";
 public static final String ACTION_AGRIDENT_READ = "fr.coppernic.tools.agrident.wedge.READ";
 public static final String KEY_BARCODE_DATA = "BarcodeData";
 ```
