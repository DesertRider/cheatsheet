# Bash

## Alias, fonctions et variables d'environnement utiles

```bash
alias dir='ls -lah'
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
```

**NOTE**
   On peut outrepasser un alias en débutant la commande voulue avec un "\\\"
   
## Variables Bash relatives au process

   * "$$" est le current pid 
   * "$!" est le pid du dernier process lancé en bg
   
   
## Utilisation d'une variable basée sur la date pour des fichiers de backups par exemple:
```bash
NOW=$(date +"%F_%Hh%M")
```

## Bash FOR loop examples
```bash
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
```
voir cette [référence sur les boucles bash[(https://www.cyberciti.biz/faq/bash-for-loop/)

## Script bash en mode debug
```bash
bash -x script.sh
```
## Durée d'exécution dans BASH avec la variable spéciale SECONDS
```bash
SECONDS=0
# do some work
duration=$SECONDS
echo "$(($duration / 60)) minutes and $(($duration % 60)) seconds elapsed."
```
## Durée d'exécution d'une commande
```bash
time du -sh /
```
## History avec date time
```bash
# dans /etc/bashrc ou mieux, dans /etc/profile.d/history.sh
cat >> /etc/profile.d/history.sh <<FIN
HISTTIMEFORMAT=\${HISTTIMEFORMAT:-"%F %H:%M:%S "}
FIN
```
## Mettre en minuscule le contenu d'une variable
```bash
NOM=`echo $NOM | tr  '[:upper:]' '[:lower:]' `
```
## Ignorer certaines lignes dans le history
```bash
echo $HISTCONTROL
# si ignorespace alors ignore les lignes débutant par un espace
# si ignoredups alors ignore les lignes en double (même commandes plusieurs fois en lignes)
# si ignoreboth alors ces deux cas
```
## Couleurs
```bash
# le fichier /etc/DIR_COLOR contient les codes de couleurs utilisés par la commande ls 
# et des indications pour les codes de couleurs
# pour mettre de la couleur dans un fichier de texte (ici rouge sur fond noir)
echo -en "\033[31;40m" >> /etc/motd
echo "Attention à ce que vous faites..." >> /etc/motd
echo -en "\033[0m" >> /etc/motd
```
## Activer pgup/pgdn search dans history
```bash
cat >> /etc/inputrc <<EOF
"\e[5~": history-search-backward
"\e[6~": history-search-forward
EOF
bind -f /etc/inputrc
# pour reloader ce fichier ou redémarrer la session
# Pour lister les binds actuels:
bind -p
```
## Complétition

Completition pour nom de répertoire ou de fichier::
```bash
complete -d cd
complete -f vim
```
**Voir aussi /etc/bash_completion.d/**

## Redirections
```bash
#  redirection de stderr
ps 2>x.err
# redirection de stderr au même fichier que stdout
ps >output.txt 2>&1
# redirection de stdout à l'écran et dans fichier
ps |tee both.txt
# redirection de plusieurs commandes
(pwd; ls) >content.txt
# redirection lorsque pas root
echo "/dev/sdb1  /data   ext4   defaults,rw   0  0" | sudo tee -a /etc/fstab
```
## Command Editing Shortcuts

* Ctrl + a – go to the start of the command line
* Ctrl + e – go to the end of the command line
* Ctrl + k – delete from cursor to the end of the command line
* Ctrl + u – delete from cursor to the start of the command line
* Ctrl + w – delete from cursor to start of word (i.e. delete backwards one word)
* Ctrl + y – paste word or text that was cut using one of the deletion shortcuts (such as the one above) after the cursor
* Ctrl + xx – move between start of command line and current cursor position (and back again)
* Ctrl-x Ctrl-e copie la ligne actuelle et ouvre l'éditeur $EDITOR pour ensuite l'exécuter

* Alt + b – move backward one word (or go to start of word the cursor is currently on)
* Alt + f – move forward one word (or go to end of word the cursor is currently on)
* Alt + d – delete to end of word starting at cursor (whole word if cursor is at the beginning of word)
* Alt + c – capitalize to end of word starting at cursor (whole word if cursor is at the beginning of word)
* Alt + u – make uppercase from cursor to end of word
* Alt + l – make lowercase from cursor to end of word
* Alt + t – swap current word with previous
* Alt-. print last argument from previous command (note: !$ sur la ligne de commande fait la même chose)

* Ctrl + f – move forward one character
* Ctrl + b – move backward one character
* Ctrl + d – delete character under the cursor
* Ctrl + h – delete character before the cursor
* Ctrl + t – swap character under cursor with the previous one
