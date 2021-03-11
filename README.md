# Bus logiciel ivy

Pour en apprendre plus sur le bus logiciel ivy, regarder la présentation -> [*ici*](https://github.com/truillet/upssitech/blob/master/SRI/3A/ID/Cours/C_ivy_2.4.pdf) <- 

Au préalable, il faudra installer les paquets : **make**, **g++**, **gcc**, **libx11-dev** et **xorg**

## ivy/c sous linux (ou bash ubuntu sous windows)
Ouvrir un nouveau terminal

Télécharger [prcre-7.7](https://github.com/truillet/ivy/blob/master/lib/pcre-7.7.zip) (*P*erl *C*ompatible *R*egex *E*xpression) et dézipper les fichiers dans le répertoire **pcre-7.7**

Télécharger [ivy C](https://github.com/truillet/ivy/blob/master/lib/ivy.zip) et dézipper les fichiers dans le répertoire **ivy**

Utiliser les commandes suivantes : compiler la librairie PCRE puis ivy
```cd prce-7.7
./configure
make
sudo make install
export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
cd ../ivy
make
```
Vous pouvez maintenant essayer l'outil *ivyprobe*

```
./ivyprobe "^(.*)"
```

Il est temps maintenant de coder votre première application ivy/C. 

Le principe d'usage est assez simple : 
* On initialise l'agent sur le bus (**IvyInit**)
* On définit les appels aux fonctions callbacks (**IvyBindMsg**) à l'aide de [regex - Regular Expresssion](https://regexr.com) 
* On enregistre l'agent sur le bus **IvyStart**) à l'adire d'une adresse ip, de broadcast et un port d'écoute
* On lance la mainloop (**IvyMainLoop**)

"et voilà" ! 

Récupérer le code [*ici*](https://github.com/truillet/ivy/blob/master/code/example_c.zip).

Décompresser le fichier, aller dans le répertoire créé

Recopier les fichiers libivy.a et libprce.a précédemment compilés dans ce répertoire.


````
gcc Ecoute.c libivy.a libpcre.a -o Ecoute
./Ecoute
````
## ivy/c#
La [dll ivy](https://github.com/truillet/ivy/blob/master/lib/ivy_csharp_dll.zip) pour C# (x86 et x64)

*[Un exemple de code ivy avec C#](https://github.com/truillet/ivy/blob/master/code/ppilot_src.zip)* et *[l'exécutable associé](https://github.com/truillet/ivy/blob/master/lib/ppilot5_v3.2.zip)*

## ivy/java (et Processing)
Le lien vers la librairie Java : [ivy-java 12.18](https://github.com/truillet/ivy/blob/master/lib/ivy-java-1.2.18.jar) ou [ivy-java 12.17](https://github.com/truillet/ivy/blob/master/lib/ivy-java-1.2.17.jar)

La [Javadoc est téléchargeable ici](https://github.com/truillet/ivy/blob/master/lib/javadoc-ivy-1.2.18.zip)

**Pour lancer Probe java** : 
```
java -cp .;ivy-java-1.2.18.jar fr.dgac.ivy.tools.Probe "^(.*)" -b 127.255.255.255:2010
```
(ou télécharger l'outil [ici](https://github.com/truillet/ivy/blob/master/code/Probe.zip))

**Un superviseur graphique des agents ivy** [visionneur](https://github.com/truillet/ivy/blob/master/lib/visionneur_1_2.zip)

*Un exemple de programme ivy avec Processing.org* : [ivySender et ivyReceiver](https://github.com/truillet/ivy/blob/master/code/ivyP5.zip) 

## ivy/python
La librairie pour Python : [ivy-python](https://pypi.org/project/ivy-python) (v.3.3 au 02/02/2021) ou [lien Gitlab](https://gitlab.com/ivybus/ivy-python)

**Pour installer la librairie (Python3)** : 
```
sudo pip3 install ivy-python
```

*Un exemple de programme ivy avec python2* : [ivyfirst.py](https://github.com/truillet/upssitech/blob/master/SRI/3A/ID/TP/Code/ivyfirst.py)

*Un exemple de programme ivy avec python3* : [ivyfirst3.py](https://github.com/truillet/ivy/blob/master/code/ivyfirst3.py)

## ivy/nodeJS
La librairie pour nodeJS-javascript : [node-ivy](https://github.com/nilpotence/node-ivy)
