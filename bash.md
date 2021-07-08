# Bash

## Alias, fonctions et variables d'environnement utiles

  >alias dir='ls -lah'
   alias ..='cd .."
   alias .."cd ../..'
   alias motd='cat /etc/motd'
   function xdiff() { file=$(readlink -e $1) ; ssh $2 "cat $file" | diff -y -W $COLUMNS "$file" - ; }
   export GREP_OPTIONS=--color
   export HISTSIZE=
   export EDITOR=vim
   export PROMPT_COMMAND='history -a'

   # Alias si pas root pour certaines commandes (*dans ~/.bashrc par exemple*)
   if [ $UID -ne 0 ]; then
       alias reboot='sudo reboot'
       alias update='sudo apt-get upgrade'
   fi


**NOTE**
   On peut outrepasser un alias en débutant la commande voulue avec un "\\\"
   
Variables Bash relatives au process::

   "$$" est le current pid 
   "$!" est le pid du dernier process lancé en bg
   
   
Utilisation d'une variable basée sur la date pour des fichiers de backups par exemple:

   NOW=$(date +"%F_%Hh%M")

## Bash FOR loop examples

   for VARIABLE in 1 2 3 4 5 .. N
   do
	   command1
	   command2
	   commandN
   done

   for VARIABLE in file1 file2 file3
   do
	   command1 on $VARIABLE
	   command2
	   commandN
   done

   for OUTPUT in $(Linux-Or-Unix-Command-Here)
   do
	   command1 on $OUTPUT
	   command2 on $OUTPUT
	   commandN
   done

voir cette [référence sur les boucles bash[(https://www.cyberciti.biz/faq/bash-for-loop/)

## Script bash en mode debug

   bash -x script.sh

## Durée d'exécution dans BASH avec la variable spéciale SECONDS

   SECONDS=0
   # do some work
   duration=$SECONDS
   echo "$(($duration / 60)) minutes and $(($duration % 60)) seconds elapsed."

## Durée d'exécution d'une commande

   time du -sh /

## History avec date time

   # dans /etc/bashrc ou mieux, dans /etc/profile.d/history.sh
   cat >> /etc/profile.d/history.sh <<FIN
   HISTTIMEFORMAT=\${HISTTIMEFORMAT:-"%F %H:%M:%S "}
   FIN

## Mettre en minuscule le contenu d'une variable

   NOM=`echo $NOM | tr  '[:upper:]' '[:lower:]' `

## Ignorer certaines lignes dans le history

   echo $HISTCONTROL
   # si ignorespace alors ignore les lignes débutant par un espace
   # si ignoredups alors ignore les lignes en double (même commandes plusieurs fois en lignes)
   # si ignoreboth alors ces deux cas

## Couleurs

   # le fichier /etc/DIR_COLOR contient les codes de couleurs utilisés par la commande ls 
   # et des indications pour les codes de couleurs
   # pour mettre de la couleur dans un fichier de texte (ici rouge sur fond noir)
   echo -en "\033[31;40m" >> /etc/motd
   echo "Attention à ce que vous faites..." >> /etc/motd
   echo -en "\033[0m" >> /etc/motd

## Activer pgup/pgdn search dans history

   cat >> /etc/inputrc <<EOF
   "\e[5~": history-search-backward
   "\e[6~": history-search-forward
   EOF
   bind -f /etc/inputrc
   # pour reloader ce fichier ou redémarrer la session
   # Pour lister les binds actuels:
   bind -p

## Complétition

Completition pour nom de répertoire ou de fichier::

   complete -d cd
   complete -f vim

**Voir aussi /etc/bash_completion.d/**

## Redirections

* ``ps 2>x.err`` redirection de stderr
* ``ps >output.txt 2>&1`` redirection de stderr au même fichier que stdout
* ``ps |tee both.txt`` redirection de stdout à l'écran et dans fichier
* ``(pwd; ls) >content.txt`` redirection de plusieurs commandes
* ``echo "/dev/sdb1  /data   ext4   defaults,rw   0  0" | sudo tee -a /etc/fstab`` redirection lorsque pas root

## Ligne de commande:

* Ctrl-A moves the cursor to the beginning of the command line
* Ctrl-E moves the cursor to the end of the command line
* Ctrl-K shortcut deletes everything immediately after the cursor
* Alt-B moves backward 1 word
* Alt-F moves forward 1 word
* Alt-D shortcut deletes the word next to the cursor
* Alt-T swap 2 words
* Alt-. print last argument from previous command
* Ctrl-Y undo a deletion  (yank)
* Ctrl-x Ctrl-e copie la ligne actuelle et ouvre l'éditeur $EDITOR pour ensuite l'exécuter

