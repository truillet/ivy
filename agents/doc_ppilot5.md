# Utiliser ppilot5
**[ppilot5](https://github.com/truillet/ivy/blob/master/agents/ppilot5_3.3.zip)** permet d’utiliser des systèmes de synthèse vocale compatibles SAPI5.

## Lancement de l’agent en ligne de commandes
```
ppilot5 -b 127.255.255.255:2010 -r Hortense -o "Microsoft Hortense"
```
Par défaut, **[ppilot5](https://github.com/truillet/ivy/blob/master/agents/ppilot5_3.3.zip)** utilise le premier moteur de TTS trouvé et apparaît sur le bus ivy sous le nom **ppilot5**

* **-b** adresse IP + port
* **-r** nom sous lequel apparaîtra l’agent sous ivy (dans l’exemple précédent, "Hortense")
* **-o** nom du moteur de synthèse utilisé (ici, la TTS "Microsoft Hortense", TTS par défaut sous windows)

### Commandes (UNIQUEMENT sur le [bus ivy](https://github.com/truillet/ivy))

#### Synthèse
* **ppilot5 Say=** hello	ppilot5 prononce via la TTS utilisée la chaîne de caractères "hello"
* **ppilot5 SaySSML=** *<sequence_SSML>*	ppilot5 prononce la séquence SSML et renvoie *ppilot5 Answer=Finished* quand le buffer est vide. Les balises <speak> et </speak> sont automatiquement ajoutées au flux	

**Exemple de séquence SSML :** 
ppilot5 SaySSML=Je peux parler \<emphasis level="strong"\>très fort\</emphasis\> si je veux !

#### Commandes
* **ppilot5 Command=Stop**	la synthèse vocale est stoppée. ppilot5 renvoie ppilot Answer=Stopped
* **ppilot5 Command=Pause**	la synthèse vocale est mise en pause. ppilot5 renvoie ppilot5 Answer=Paused
* **ppilot5 Command=Resume**	la synthèse vocale est relancée si elle était en pause précédemment. ppilot5 renvoie ppilot5 Answer=Resumed
* **ppilot5 Command=Quit**	l’application se ferme

#### Paramètres
* **ppilot5 Param=Pitch:** value	le pitch est changé par la valeur donnée. ppilot5 renvoie ppilot5 Answer=PitchValueSet:value
* **ppilot5 Param=Speed:** value	la vitesse est changée par la valeur donnée. ppilot5 renvoie ppilot5 Answer=SpeedValueSet:value
* **ppilot5 Param=Volume:** value le volume est changé par la valeur donnée. ppilot5 renvoie ppilot5 Answer=VolumeValueSet:value
