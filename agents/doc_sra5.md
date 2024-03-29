# Utiliser sra5
**[sra5](https://github.com/truillet/ivy/blob/master/agents/sra5.zip)** est un agent utilisant le moteur de reconnaissance natif SAPI 5.x de Windows Vista, 7, 8.1 ou 10 et peut renvoyer deux types de solutions issues de la reconnaissance sous deux formats différents : sous forme de séquence orthographique ou sous forme de concepts.

## Lancement de l’agent en ligne de commandes
```
sra5 -b 127.255.255.255:2010 –p on -g grammaire.grxml
```
Par défaut, **[sra5](https://github.com/truillet/ivy/blob/master/agents/sra5.zip)** utilise le fichier de grammaire locale *grammaire.grxml*

* **-b** : adresse IP + port
* **-p** : mode de renvoi des données (mode parsage *on* ou *off*) - Le mode *parsage* consiste à renvoyer comme résultat les <ins>sorties sémantiques</ins> plutôt que la chaîne orthographique.
* **-g** : fichier de grammaire utilisé (grammaire de type [grXML](http://www.w3.org/TR/speech-grammar))

### Commandes (UNIQUEMENT sur le [bus ivy](https://github.com/truillet/ivy))
* **sra5 -p** {*on* | *off*} : sra5 change le mode de retour de la reconnaissance (*on* --> mode de retour sous forme de concept ou *off* --> mode de retour orthographique)
* **sra5 –g** *nom_grammaire.grxml* : sra5 active une nouvelle grammaire *nom_grammaire.grxml* (sur un chemin local à la machine)

### Retours (UNIQUEMENT sur le [bus ivy](https://github.com/truillet/ivy))
* **sra5 Text**=chaîne_orthographique **Confidence**=taux_de_confiance (si le flag *parse* est positionné à *off*)
* **sra5 Parsed**=resultat **Confidence**=taux_de_confiance **NP**=xx **Num_A**=xx où *NP* est le numéro du résultat courant et *Num_A* le numéro d’alternative (si le flag parse est positionné à *on*)
* **sra5 Event**={*Grammar_Loaded* | *Speech_Rejected*} : *envoi d’événements provenant du moteur de reconnaissance.*
