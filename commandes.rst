Commandes
=========

find
----

Chercher avec case insensitive du name::

   find . -iname log4j* -ls

Trouver les fichiers modifié depuis moins d'un jour::

   find . -mtime 0 -print

Trouver les fichiers modifiés il y a moins d'une heure::

   find . -mmin -60 -print

Pour trouver les fichiers modifiés depuis 1 jour  dans le répertoire courant::

   find . –ctime -1 –print

Pour trouver tous les fichiers modifié depuis la dernière semaine::

   find . -ctime -7 -print

Trouver un répertoire avec le nom erreur::

   find / -type d -name erreur

Faire un find + print detailed infos sur les fichiers trouvés::

   find . -name authorized_keys -exec ls -l '{}' \;

Faire un dir récursif avec détails::

   find . -exec ls -l '{}' \;
   # ou
   find . -type f -printf '%p\n'

Lister les fichiers plus vieux de 30 jours::

   find . -mtime +30 -exec ls '{}' \;

Faire du ménage des fichiers plus vieux de 30 jours::

   find . -mtime +30 -exec rm '{}' \;

Lister les fichiers créés aujourd´hui::

   find -maxdepth 1 -type f -mtime -1

Trouver les fichier d'un utilisateur::

   find /var -user www-data

Limiter la profondeur de recherche à 2 niveaux de répertoires::

   find -maxdepth 2 -name *.conf
   # (on peut faire un mindepth aussi)

Inverser la recherche::

   find -maxdepth 1 -not -iname *.c

Trouver les fichiers pas d'un certain user::

   find . \! -user root -print

Faire un find avec logical or::

   find / \( -iname snap.*.trc -o -iname core.*.dmp -o -iname heapdump.*.phd -o -iname javacore.*.txt \) -print

Faire un find avec exclusion de répertoire::
   find / -path /media/nss -prune -o \( -iname snap.*.trc -o -iname core.*.dmp -o -iname heapdump.*.phd -o -iname javacore.*.txt \) -print  

Trouver les fichiers récents plus gros que 500M::

   find / -type f -size +500M -ctime -1 -exec  ls -l '{}' \;

Trouver les programmes qui ont le bit setuid ou setgid activé::

   find / -xdev -type f -perm +ug=s -exec ls -ldb {} \;


vim
---

Commandes de disques, partitions, ...
-------------------------------------

yum
---
