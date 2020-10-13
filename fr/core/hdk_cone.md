HDK pour C-One
=============

Si vous ne savez pas ce qu'est un C-One? La réponse est [ici](https://www.coppernic.fr/prehome-mobility-fr/).

L'API HDK a été conçue avec [RxJava2](https://github.com/ReactiveX/RxJava).

Prérequis
---------

Pour la première génération de produits, l'application **CpcSystemServices** à la version 2.1.0 ou supérieure doit être installée sur le terminal.
Pour la [seconde génération](/fr/quickstart.md) **CoreService** doit être installée au lieu de **CpcSystemServices**.
Vous pouvez contacter le [Support Coppernic](support@coppernic.fr) en cas de difficultés.

Utiliser les pins du port d'expansion du C-One
----------------------------------------------

* Récupérer une instance de GpioPort :

```java
private GpioPort gpioPort;

@Override
public void onStart() {
    super.onStart();
    GpioPort.GpioManager.get()
        .getGpioSingle(getContext())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(new Consumer<GpioPort>() {
            @Override
            public void accept(GpioPort g) throws Exception {
                gpioPort = g;
            }
        });
}
```

* Bagoter la pin:

```java
RESULT res = gpioPort.setPin1(true)
```

Observer l'état de la pin d'entrée
----------------------------------

```java
//Enregistrer un observer sur l'état de la pin d'entrée
Disposable d = GpioPort.observeInputPin4(getContext(), 200, TimeUnit.MILLISECONDS)
                // Be notified only when value is changing
                .distinctUntilChanged()
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new Consumer<Boolean>() {
                    @Override
                    public void accept(Boolean aBoolean) throws Exception {
                        //Do something
                    }
                });
//Disposer l'observer quand vous avez fini
d.dispose()
```
