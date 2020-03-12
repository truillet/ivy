# Bus logiciel ivy

## ivy/c sous linux (ou bash ubuntu sous windows)

Télécharger [prcre-7.7](https://github.com/truillet/ivy/blob/master/lib/pcre-7.7.zip) (*P*erl *C*ompatible *R*egex *E*xpression) et dézipper les fichiers dans le répertoire pcre-7.7
Télécharger [ivy C](https://github.com/truillet/ivy/blob/master/lib/ivy.zip) et dézipper les fichiers dans le répertoire ivy
Utiliser les commandes suivantes : compiler la librairie PCRE
```cd prce-7.7\n
./configure
make
sudo make install
export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
```


