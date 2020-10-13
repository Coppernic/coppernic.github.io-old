Qualité
=======

## Généralités

Durant le développement de votre application sur notre terminal, merci de suivre les recommandations de Google:

[Qualité des applications](https://developer.android.com/docs/quality-guidelines/core-app-quality)

Merci de lire aussi le document de Google sur [l'optimisation de la durée de vie de la batterie](https://developer.android.com/topic/performance/power)

## RFID

La recherche d'une carte (Chasse) peut être consommateur de courant. Veuillez mettre en place
toutes les solutions que vous jugerez utile pour réduire le temps d'utilisation de votre lecteur RFID.

Par exemple, durant le temps de chasse, le champ électromagnétique peut être alimenté pendant 200ms puis éteint pendant 800ms.
Ces paramètres assurent que l'expérience utilisateur ne sera pas affecté et préserve l'autonomie de la batterie.

Assurez-vous lorsque l'écran s'éteint ou quand l'utilisateur quitte votre application (ou les écrans liés à la RFID),
que tous les périphériques s'éteignent également.
