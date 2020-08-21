Key Mapping
===========

## API de CpcCore 1.8.0 (package `mapping`)

Cette API est conçue pour fonctionner sur tous les produits Coppernic (Actuellement C-One, C-five et C-One²), et sur tous les OS.
Mais vous devez garder à l'esprit que cette API utilise en interne différentes API qui peuvent avoir des limites.

Par exemple, pour avoir le mapping actuel sur C-five, vous devez au moins avoir la version d'OS v20180709.

Cette API est complètement implémentée sur:

  - C-five OS v20180928
  - C-One² OS v20180907

Tous les autres OS et C-One sont aussi compatibles mais il peut y avoir des limites. Testez l'API dont vous avez besoin et contactez le [Support Coppernic](support@coppernic.fr) si vous avez besoin d'aide.

### Obtenir un objet `Mapper`

La première chose à faire est d'obtenir un objet `Mapper`. Une connexion au service est requise donc obtenir cette référence doit être faite de manière asynchrone. RxJava est ici pour nous aider:

```java
Mapper.Factory.getKeyMapperSingle(context)
                 .subscribe(new DisposableSingleObserver<Mapper>() {

            @Override
            public void onSuccess(Mapper km) {
                // you can store a reference for a later use
                mapper = km;
            }

            @Override
            public void onError(Throwable e) {
                // Handle the error here
            }
        });
```

### Mapping

#### Import

```java
import fr.coppernic.sdk.mapping.Mapper;
import fr.coppernic.sdk.mapping.Mapper.MappingType;
import fr.coppernic.sdk.mapping.utils.MapperUtils;

import static fr.coppernic.sdk.mapping.Mapper.ProgKey.P1;
import static fr.coppernic.sdk.mapping.Mapper.ProgKey.P2;
import static fr.coppernic.sdk.mapping.Mapper.ProgKey.P3;
```

#### Prog keys

Les valeurs des touches programmables sont définies dans l'enum `Mapper.ProgKey`.

#### API

```java
// Suppression de l'association du bouton 1
mapper.remove(P1);
// Suppression de l'association du bouton 2
mapper.remove(P2);
// Suppression de l'association du bouton 3
mapper.remove(P3);

// Suppression de toutes les associations 
mapper.removeAll();

// Associer une touche
mapper.mapKey(P1, KeyEvent.KEYCODE_1);
mapper.mapKey(P2, KeyEvent.KEYCODE_2);
mapper.mapKey(P3, KeyEvent.KEYCODE_3);

// Obtenir l'association actuelle
assertThat(mapper.getKeyMapping(P1), is(KeyEvent.KEYCODE_1));
assertThat(mapper.getKeyMapping(P2), is(KeyEvent.KEYCODE_2));
assertThat(mapper.getKeyMapping(P3), is(KeyEvent.KEYCODE_3));
assertThat(mapper.getMappingType(P1), is(MappingType.KEY));
assertThat(mapper.getMappingType(P2), is(MappingType.KEY));
assertThat(mapper.getMappingType(P3), is(MappingType.KEY));

// Associer la touche P1 à BARCODE_SCAN
mapper.mapKey(P1, MapperUtils.getBarcodeMappingKeyCode());

// Associer un raccourcis
mapper.mapShortcut(P1, context, "com.google.android.youtube");
assertThat(mapper.getShortcutMapping(P1), is("com.google.android.youtube"));
assertThat(mapper.getMappingType(P1), is(MappingType.SHORTCUT));

//Quand vous en avez fini avec l'objet `Mapper`
mapper.close();
```
### Cas spéciaux pour Barcode

#### C-One²

L'API est stable à partir de l'OS v20180907

- Associer une touche à BARCODE_SCAN: `mapper.mapKey(P1, MapperUtils.getBarcodeMappingKeyCode())`
- Obtenir la valeur de BARCODE_SCAN: `assertThat(mapper.getKeyMapping(P1), is(MapperUtils.getBarcodeMappingKeyCode()));`

#### C-five

- OS v20171117:
  - `mapper.getKeyMapping()` ne fonctionne pas.
- OS v20180709:
  - Associer une touche à BARCODE_SCAN: `mapper.mapKey(P1, 293)`
  - Obtenir la valeur de BARCODE_SCAN: `assertThat(mapper.getKeyMapping(P1), is(KeyEvent.KEYCODE_BUTTON_MODE));`
- OS v20180928
  - Associer une touche à BARCODE_SCAN: `mapper.mapKey(P1, MapperUtils.getBarcodeMappingKeyCode())`
  - Obtenir la valeur de BARCODE_SCAN: `assertThat(mapper.getKeyMapping(P1), is(MapperUtils.getBarcodeMappingKeyCode()));`
