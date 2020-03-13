# Bus logiciel ivy

## ivy/c sous linux (ou bash ubuntu sous windows)
Ouvrir un nouveau terminal

Télécharger [prcre-7.7](https://github.com/truillet/ivy/blob/master/lib/pcre-7.7.zip) (*P*erl *C*ompatible *R*egex *E*xpression) et dézipper les fichiers dans le répertoire pcre-7.7

Télécharger [ivy C](https://github.com/truillet/ivy/blob/master/lib/ivy.zip) et dézipper les fichiers dans le répertoire ivy

Utiliser les commandes suivantes : compiler la librairie PCRE puis ivy
```cd prce-7.7\n
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

Il est temps maintenant de coder votre première application ivy/C (le code est [*ici*](https://github.com/truillet/ivy/blob/master/code/example_c.zip)). 

Le principe est assez simple : 
* On initialise l'agent sur le bus (**IvyInit**)
* On définit les appels aux fonctions callbacks (**IvyBindMsg**) à l'aide de [regex - Regular Expresssion](https://regexr.com) 
* On enregistre l'agent sur le bus **IvyStart**) à l'adire d'une adresse ip, de broadcast et un port d'écoute
* On lance la mainloop (**IvyMainLoop**)

"et voilà" ! 

````
gcc Ecoute.c -o Ecoute
./Ecoute
```


