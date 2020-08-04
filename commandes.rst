Commandes
=========

grep, egrep, ngrep, ...
-----------------------

Meta-char les plus utilisés pour grep
::

   ^           Beginning of the line
   $           End of the line eight
   \<          Beginning of the word
   \>          End of the word
   [abc]       matches any one of “a”, “b”, and “c”
   [a-z]       matches any one character from “a” to “z”
   [-:+]:      any one of ”-”, “:” and “+”
   [^xyz]      None of the characters
   .           Any single character file
   +           One or more of the preceding expression
   *           Any number (including none) of preceding single character
   {min,max}   The preceding expression min times at minimum
   |           The expression before or after (example: file|File: matches file and File)
   (...)       Enclose alternatives for grouping with others (example: (f|F)ile: matches file and F)
   ?           Zero or one of the preceding
   \           Escape the following metacharacter

grep des lignes non-commentées ou vides dans un fichier de configuration::

   egrep -v '^\s*#|^$' nrpe.cfg

grep avec contexte (lignes entourant l'élément trouvé)::

   grep -A pour --after-context=NUM
   grep -B pour --before-context=NUM
   grep -C pour --context=NUM

grep pipe dans less et utilisation de couleurs::

   grep --color=always "Alias" fichier| less -R
   # ou dans less, taper -R
   # ou utiliser la variable d'environnement LESS comme suit
   export LESS=-R

grep des lignes non-commentées ou vides dans un fichier de configuration::

   egrep -v '^\s*#|^$' nrpe.cfg

grep avec no de la ligne trouvée::

   grep -nr toto fichier

Voir le contenu d'un fichier à partir d'un grep jusqu'à la fin::

   tail -n +$(grep -n -m 1 "Jan 15 11:10" /var/log/postfix.log | cut -f1 -d:) /var/log/postfix.log |less



grep de tcpdump::

   yum install -y ngrep
   ngrep -W byline "X-Forwarded-For: 192.168.200.241" port 80


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


rsync
-----

synchronisation entre 2 répertoires local::

   rsync -av --delete /zcm/ /zcm2/

   # avec -i output a change-summary for all updates
   rsync -a -i --delete --log-file=/var/log/rsync-data2.log /media/nss/DATA2/ /media/nss/DATA2NEW/
   
   # avec -x reste sur le même file system (utile pour copier / mais pas /var si sur un 2e disque)
   # avec --dry-run, affichage de ce qui serait fait seulement, pas d'action
   rsync -avx --dry-run -delete / /mnt/new

rsync entre 2 serveurs::

   rsync -av --delete -e ssh /home1 root@qxdnfs20:/home1


vim
---

::

   */#					search next/prev occurence of word under cursor
   hjkl				déplacement gauche, bas, haut, droit
   w/b					saut avant/arrière au début du prochain mot
   f/F					cherche avant/arr. du prochain car tapé sur la ligne
   dw/cw				delete/change word
   rx					change le car. sous le curseur par x
   9G					va à la ligne 9
   /{up}				search history
   /.pache	wildcard	dans recherche
   :s/1/2/g			remplace 1 par 2 pour la ligne
   :%s/1/2/g			remplace 1 par 2 pour toutes les lignes
   :%s/1/2/gi			remplace 1 par 2 pour toutes les lignes, case ins.
   :%s/1/2/gc			rempl. 1 par 2 pour toutes les lignes avec conf.
   :1,$s/1,2,/g        remplace 1 par 2 pour toutes les lignes (identique à :%s/1/2/g)
   :.,$s/1,2,/g        remplace 1 par 2 pour la ligne courante jusqu'à la fin du document

   :set [no]number		affiche les numéros de ligne ou pas
   :set [no]hlsearch	highlight search oui/non
   :nohlsearch			désactive le highlight du search courant seul.
   :set viminfo+=/0	désactive search history
   :set smartcase		pour search case insensitive
   :set [no]ignorecase	recherche case sensitive ou pas
   :edit fichier       pour ouvrir un second fichier
   :set formatoptions-=r pour empêcher les commentaires "#" de se continuer automatiquement sur une nouvelle ligne après un Enter
   :set wrap!          pour arrêter le wrap des lignes longues

   #delete from here to end of file:
   dG
   #record macro in register "a"
   qa(actions)q
   #playback macro in register "a" 10 times
   10@a
   #repeat macro until end of file
   :%normal @a




yum, RPM
--------

Installation de EPEL::

   yum install epel-release

yum pour télécharger package et dépendances + installation locale::

   # attention: fait le download de toutes les dépendances, aucune vérification si elles sont déjà installées ou pas
   yum repotrack mutt
   yum localinstall mutt

yum pour chercher qui fournit tel programme::

   yum provides javac

yum désinstallation d'un ou plusieurs packages::

   yum remove tomcat*

yum download and install all available security updates::

   yum -y update --security

yum download only package::

   yum install vsftpd --downloadonly --downloaddir=/tmp

historique de yum::

   yum history

yum update sauf certains package::

   yum update --exclude kernel

yum list les packages et repository d'où il provient::

   yum list installed *openjdk*

voir les script du package ou fichier::

   rpm -q --scripts httpd
   rpm -qp --scripts filename.rpm

apt-get, apt-cache, etc (Debian)
--------------------------------

Affichage du package gammu installé::

   apt-cache show gammu

Update packages::

   apt-get update

Installation de netcat::

   apt-get install netcat

Retirer un package sans leur retirer leur fichiers de configuration::

   apt-get remove vsftpd

Retirer au complet le package::

   apt-get purge vsftpd
   ou
   apt-get remove --purge vsftpd
   
Clean du cache::

   apt-get clean all


