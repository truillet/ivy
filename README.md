# Bus logiciel ivy / ivy middleware <img src="https://github.com/truillet/ivy/blob/master/doc/ivylogo.jpg" width=80>
Ivy est un [bus logiciel](http://www.eei.cena.fr/products/ivy) conçu à la DTI R&D (ex CENA) dans le but de connecter d’une manière extrêmement simple des applications interactives ou pas en elles écrites avec différents langages et fonctionnant sur différentes machines ou plates-formes.

Il s’agit d’un modèle de communication compatible avec la programmation événementielle classique des interfaces graphiques. En un sens, ce bus logiciel implémente une approche multi-agents : les agents apparaissent, émettent des messages et en reçoivent, les traitent puis quittent le bus sans bloquer les autres agents présents. Ivy vise principalement à faciliter le développement rapide de nouveaux agents, et à en contrôler une collection dynamique. Par opposition à certains autres bus logiciels, ivy ne se fonde pas sur un serveur central ou un annuaire qui permet de *router* les demandes d’un agent. Au lancement, tous les agents se présentent à un point de rendez-vous, le reste est transparent pour le programmeur !

**A quoi cela peut-il bien servir ?** Bien que limité à des échanges de messages textuels, ce principe permet de prototyper très rapidement (en ré-utilisant des agents déjà développés) voire de concevoir des systèmes adaptés spécifiquement aux besoins d’une personne, tout cela indépendamment du système.

Pour en apprendre plus sur le bus logiciel ivy :
* regarder la présentation -> [**ici**](https://github.com/truillet/ivy/blob/master/doc/C_ivy_2.8.pdf) <- ou l'article publié à **[IHM 2012](https://hal-enac.archives-ouvertes.fr/hal-00940960/document)**
* quelques éléments sont aussi disponibles sur [GitLab](https://gitlab.com/ivybus) et/ou [gitpub](https://gitpub.recherche.enac.fr/ivy).
* vous pourrez enfin aussi trouver des informations sur le site du projet *[Paparazzi](https://wiki.paparazziuav.org/wiki/Ivy)*

Vous trouverez ci-dessous des outils et les librairies nécessaires à l'écriture des agents ivy.

## Un "superviseur" du middleware (pour suivre l'émission/réception des messages ivy)
Le superviseur est un outil ivy et a pour objet de suivre les agents connectés, envoyer des messages afin de simuler les messages envoyés par des agents.

**Un supervisieur du middleware est disponible en mode CLI - Probe (java)** : 
```console
java -cp .;ivy-java-1.2.18.jar fr.dgac.ivy.tools.Probe "^(.*)" -b 127.255.255.255:2010
```
(ou télécharger l'outil Probe **[ici](https://github.com/truillet/ivy/blob/master/code/Probe.zip)**)

**Un superviseur du middleware en mode GUI - visionneur (java) est disponible ici :** [visionneur.zip v 1.2](https://github.com/truillet/ivy/blob/master/lib/visionneur_1_2.zip)

## librairie ivy/c
### compiler et utiliser la livrairie ivy/c sous linux (ou bash ubuntu sous windows)
Ouvrir un nouveau terminal

Au préalable, il faudra installer les paquets : **make**, **g++**, **gcc**, **libx11-dev** et **xorg**

Télécharger [prcre-7.7](https://github.com/truillet/ivy/blob/master/lib/pcre-7.7.zip) (*P*erl *C*ompatible *R*egex *E*xpression) et dézipper les fichiers dans le répertoire **pcre-7.7**

Télécharger [ivy.zip](https://github.com/truillet/ivy/blob/master/lib/ivy.zip) et dézipper les fichiers dans le répertoire **ivy** (Vous pouvez aussi trouver le code source ->**[ici](https://gitlab.com/ivybus/ivy-c)**<-

Utiliser les commandes suivantes : compiler la librairie PCRE
```console
unzip pcre7.7.zip
cd pcre-7.7
chmod 777 ./configure
./configure
sudo make install
export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
```
Les librairies PCRE compilées sont stockées dans le répertoire **.libs**. Compiler maintenant la librairie ivy 

```console
cd ..
unzip ivy.zip
cd ivy
make
```
Vous pouvez maintenant essayer l'outil *ivyprobe* en lançant la commande

```console
./ivyprobe "^(.*)"
``
Par défaut, ivy se lance sur l'adresse 127.255.255.255:2010 (adresse de broadcast "127.255.255.255" sur le port 2010). Rien ne vous empêche d'en changer 😉 : adresse IP , adresse de broadcast ou de multicast (Ex : 224.0.0.0:2010) [utile si vous voulez connecter vos applications entre windows et WSL2].

Il est temps maintenant de coder votre première application ivy/C. 

Le principe d'usage est assez simple : 
* On initialise l'agent sur le bus (**IvyInit**)
* On définit les appels aux fonctions callbacks (**IvyBindMsg**) à l'aide de [regex - Regular Expresssion](https://regexr.com) 
* On enregistre l'agent sur le bus **IvyStart**) à l'adire d'une adresse ip, de broadcast et un port d'écoute
* On lance la mainloop (**IvyMainLoop**)

"et voilà" ! 

Récupérer le code [*ici*](https://github.com/truillet/ivy/blob/master/code/example_c.zip).

Décompresser le fichier, aller dans le répertoire créé (par exemple *ivy_exemple*).

Recopier les fichiers **libivy.a** (depuis le répertoire *ivy*) et **libpcre.a** (depuis le répertoire *pcre7.7/.libs*) précédemment compilés dans ce répertoire.
```console
cd ~/cd ivy_exemple
cp ~/prce7.7/.libs/libpcre.a .
cp ~/ivy/libivy.a .
```
Compiler le code

```console
gcc Ecoute.c libivy.a libpcre.a -o Ecoute

./Ecoute
```
**Ecoute** est abonné aux messages suivants : *tous '(.\*)'* et *Bye* (qui permet de quitter l'application)

**[Lien 1 vers le code source](https://github.com/lii-enac/libivy)** ou **[Lien 2 vers le code source](https://github.com/lii-enac/libivy](https://gitlab.com/ivybus/ivy-c)**


## librairie ivy/c#
La [dll ivy](https://github.com/truillet/ivy/blob/master/lib/ivy_csharp_dll.zip) pour C# (x86 et x64)

*[Un exemple de code ivy avec C#](https://github.com/truillet/ivy/blob/master/code/ppilot_src.zip)* et *[l'exécutable associé](https://github.com/truillet/ivy/blob/master/lib/ppilot5_v3.2.zip)*

## librairie ivy/java (et Processing.org)
Le lien vers la librairie Java : [ivy-java 1.2.18](https://github.com/truillet/ivy/blob/master/lib/ivy-java-1.2.18.jar) ou [ivy-java 1.2.17](https://github.com/truillet/ivy/blob/master/lib/ivy-java-1.2.17.jar)

La [Javadoc est téléchargeable ici](https://github.com/truillet/ivy/blob/master/lib/javadoc-ivy-1.2.18.zip)

* Un exemple de programme ivy avec Processing.org* : [ivySender et ivyReceiver](https://github.com/truillet/ivy/blob/master/code/ivyP5.zip) 

**[Lien vers le code source](https://gitlab.com/ivybus/ivy-java)**

## librairie ivy/nodeJS
La librairie pour nodeJS-javascript : [node-ivy](https://github.com/nilpotence/node-ivy) ou sur [NPM](https://www.npmjs.com/package/node-ivy)

## librairie ivy/OCaml
La librairie pour OCaml : [ivy/ocaml](https://gitlab.com/ivybus/ivy-ocaml)

## librairie ivy/python
La librairie pour Python :  [ivy-python 4.0](https://pypi.org/project/ivy-python) (v.4.0 au 05/10/2023) ou [lien Gitlab](https://gitlab.com/ivybus/ivy-python) (**[documentation](https://ivy-python.readthedocs.io/en/latest/index.html)**) ou [ [ivy-python 3.3](https://pypi.org/project/ivy-python/3.3) (v.3.3 au 02/02/2021) [_compatible Python 2.7_]

**Pour installer la librairie (Python3) - version stable 4.0** : 
```console
sudo pip3 install ivy-python==4.0
```
*Un exemple de programme ivy avec python3* : [ivyfirst3.py](https://github.com/truillet/ivy/blob/master/code/ivyfirst3.py)

*Un exemple de programme ivy avec python2* : [ivyfirst.py](https://github.com/truillet/upssitech/blob/master/SRI/5A/ID/TP/Code/ivyfirst.py)

## librairie ivy/Qt
La librairie pour Qt : [IvyQt](https://gitlab.com/ivybus/IvyQt)

## libraririe ivy/Rust
La librairie pour Rust : [ivy-rust](https://github.com/paparazzi/ivy-rust)

# Des passerelles entre middlewares divers
Des ponts entre différents protocoles de communication ont été écrits :
* [TUIO to ivy](https://github.com/truillet/TUIO2ivy) (Lien vers le protocole [TUIO](https://www.tuio.org))
* [ivy to ROS2](https://github.com/truillet/ivy/blob/master/code/bridge.zip) ([installation et compilation du noeud ROS](https://github.com/truillet/ivy/blob/master/doc/ROS2.md))

# Téléchargement d'agents ivy déjà développés
* [OneDollarIvy](https://github.com/truillet/OneDollarIvy) : un agent (*Processing.org*) de reconnaissance de gestes basé sur l'algorithme *"$1 recognizer"*
* [ppilot 3.3](https://github.com/truillet/ivy/blob/master/agents/ppilot5_3.3.zip) : un agent (*C#*) Text-to-Speech (SAPI5 avec support SSML) *windows* 
* [sra5](https://github.com/truillet/ivy/blob/master/agents/sra5.zip) : un agent (*C#*) de reconnaissance vocale (SAPI5, support GrXML) *windows*
* [SR_Ivy](https://github.com/truillet/tas_de_code/blob/master/Speech_Recognition/SR_ivy.py) : un agent (*python*) de reconnaissance vocale (Google Voice) *linux, macOS, windows*
* [tobiiIvy](https://github.com/truillet/ivy/blob/master/agents/tobiiIvy.zip) : un agent (*C#*) eye-tracker pour [Tobii xC](https://gaming.tobii.com/product/eye-tracker-5) *windows*
* [tobiiP5](https://github.com/truillet/ivy/blob/master/agents/tobiiP5.zip) : un exemple (*Processing.org*) d'usage de *tobiiIvy* 

# Des projets étudiants :)
* [Le kebab virtuel](https://github.com/AlexandreLanglade/kebab_virtuel)
