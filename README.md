# INF1070ETE2024-LAB6

## 1. Localisation 
 
Suivez ce qui est indiqué ! 

## 2. Création et manipulation d'archives tar ! 


créer une archive : 

```sh 
tar -c /usr/share/dict/ -f usr-dict.tar
tar: Removing leading `/' from member names
```

`-c /usr/share/dict/` : indique qu'on veut créer une archive à partir de `/usr/share/dict/` 
`-f usr-dict.tar` : donne le nom de l'archive à devoir créer ! 

Ceci donne un message qui dit que le `/` sera enlever, ceci est du au fait qu'il represente un chemin absolu ! 

`-P ` : permettrait de garder `/` au debut si on voulait 


```sh 
tar -tf usr-dict.tar
```

`-t` :  liste le contenu de l'archive ! 

créer une archive sans préfixe : 


Enlever des parties : 

```sh 
tar -cf dict.tar -C /usr/share dict/

```

`-C /usr/share ` : change temporairement de dossier (directory) pour chercher `dict/`. 


```sh 
tar -tf dict.tar 
dict/
dict/ogerman
dict/words
dict/spanish
dict/README.select-wordlist
dict/ngerman
dict/words.pre-dictionaries-common
dict/cracklib-small
dict/portuguese
dict/italian
dict/brazilian
dict/british-english
dict/french
dict/swiss
dict/american-english
```

Extraire tar : 

```sh 
tar -xf dict.tar 
```

`-x` : pour extraire ! 

Ainsi : 

```sh 
ls
dict  dict.tar  README.md  usr-dict.tar
```

Supprimer une ligne : 

```sh 
vim dict/french
```

On peut supprimer une ligne avec `dd`. 

`diff` de tar : 

```sh
tar --compare -f dict.tar dict
dict/ogerman: Uid differs
dict/ogerman: Gid differs
dict/spanish: Uid differs
dict/spanish: Gid differs
dict/README.select-wordlist: Uid differs
dict/README.select-wordlist: Gid differs
dict/ngerman: Uid differs
dict/ngerman: Gid differs
dict/cracklib-small: Uid differs
dict/cracklib-small: Gid differs
dict/portuguese: Uid differs
dict/portuguese: Gid differs
dict/italian: Uid differs
dict/italian: Gid differs
dict/brazilian: Uid differs
dict/brazilian: Gid differs
dict/british-english: Uid differs
dict/british-english: Gid differs
dict/french: Uid differs
dict/french: Gid differs
dict/french: Mod time differs
dict/french: Size differs
dict/swiss: Uid differs
dict/swiss: Gid differs
dict/american-english: Uid differs
dict/american-english: Gid differs
```

`dict/french: Size differs` : indique que la taille n'est pas la meme ! 

Note : `Uid` et `Gid` indique que l'utilisateur et le groupe sont differents entre l'archive et le dossier. 
Ceci est normal parce que l'archive est basee sur `/usr/share/` alors que le dossier nous appartient. 

Mettre a jour une archive :

```sh 
tar -u dict/ -f dict.tar
```
`-u dict/` : indique qu'on veut mettre a jour l'archive avec `dict/`. 


```sh
tar -tf dict.tar
dict/
dict/ogerman
dict/words
dict/spanish
dict/README.select-wordlist
dict/ngerman
dict/words.pre-dictionaries-common
dict/cracklib-small
dict/portuguese
dict/italian
dict/brazilian
dict/british-english
dict/french
dict/swiss
dict/american-english
dict/french
```

`dict/french` apparait 2 fois ! Ceci vient du fait que TAR vient de "tape archive". Quand on archivait sur des "tapes", ainsi, il etait tres difficile de remplacer/ modifier le contenu d'une archive. 


Supprimer un element de l'archive : 

```sh 
tar --delete dict/french -f dict.tar 
```

```sh 
tar -tf dict.tar
dict/
dict/ogerman
dict/words
dict/spanish
dict/README.select-wordlist
dict/ngerman
dict/words.pre-dictionaries-common
dict/cracklib-small
dict/portuguese
dict/italian
dict/brazilian
dict/british-english
dict/swiss
dict/american-english
```

Ajouter un element a une archive : 

```sh 
tar -r dict/french -f dict.tar
```

```sh 
tar -tf dict.tar 
dict/
dict/ogerman
dict/words
dict/spanish
dict/README.select-wordlist
dict/ngerman
dict/words.pre-dictionaries-common
dict/cracklib-small
dict/portuguese
dict/italian
dict/brazilian
dict/british-english
dict/swiss
dict/american-english
dict/french
```

## Compression : 

Comparer archive de l'originale : 
```sh 
du -b dict dict.tar
29882667	dict
29900800	dict.tar
```

`-b` : avoir le resultat en bytes/octets. 

Differents algorithmes de compressions : 

Avec: 
```sh 
bzip2 --keep dict.tar
```


```sh
29212	dict
29200	dict.tar
7488	dict.tar.bz2
6308	dict.tar.gz
4040	dict.tar.xz
```

Avec time : 

```sh 
time bzip2 --keep dict.tar; time xz --keep dict.tar; time gzip --keep dict.tar

real	0m1.228s
user	0m1.202s
sys	0m0.024s

real	0m9.068s
user	0m8.982s
sys	0m0.084s

real	0m1.253s
user	0m1.245s
sys	0m0.008s
```
`;` : permet de chainer les commandes sur une lignes, ceci n'est pas recommende... 

Correlation entre reduction de la taille et le temps pris pour compresser ! 

`tar` peut aussi compresser :

```sh
tar -zc dict/ -f dict-tar.tar.gz
```
`-z` specifie gzip pour compresser en creant l'archive !



Extraire :

```sh 
gzip -d dict.tar.gz 
gzip: dict.tar already exists; do you wish to overwrite (y or n)? y
```
`-d` pour decompresser (marche avec les autres algorithmes) !

avec `tar` : 

```sh
tar -xf dict.tar.bz2
```


## Exercice 2 : 

1) `fstab` dans `/etc/` car c'est une forme de configuration.
2) `passwd` aussi 
3) `passwd` est dans `/bin` car c'est un executable !
4) `useradd` admin systeme : `/sbin`
5) `wump` est dans `usr/games` ! 
6) `README.hunt.gz` est dans `/usr/share/doc/bsdgames` ! 

```sh
    Conrad Huang
    conrad@cgl.ucsf.edu
    Greg Couch
    gregc@cgl.ucsf.edu
    October 17, 1988
```
7) Les `log` sont dans `/var/log` ! `dpkg.log` est un log de ce qui a ete installe du plus nouveau au plus ancier `dpkg.log.1` est plus vieux ! 
8) `vmlinuz-6.8.0-76060800daily20240311-generic` (j'utilise pop-os et non une machine virtuelle) est dans `/boot`. 
