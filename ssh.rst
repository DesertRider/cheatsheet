SSH
===

Connexion ssh sans mot de passe (avec clé uniquement)
-----------------------------------------------------

::

   ssh-keygen -t rsa
   ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
 
Voir les clés publiques ssh d'un serveur
----------------------------------------

::

   ssh-keyscan qxacmsw20.pra.shq.local

Afficher le ssh server key fingerprint
--------------------------------------

::

   file=$(mktemp)
   ssh-keyscan serveur > $file 2> /dev/null
   ssh-keygen -l -f $file
   
Redirection ssh / putty (port forwarding)
-----------------------------------------

Exemple de tunnel ssh fait par putty: la console CUPS n'est accessible qu'à localhost sur le port 631
alors dans Putty on ouvre une session ssh, on modifie Connection > SSH > Tunnels, dans "Source port" on indique 631, dans Destination
on indique localhost:631

On peut maintenant accéder à la console CUPS via firefox http://localhost:631

Exemple d'accès à un serveur web sur le port 80 via notre port local 8080::

   putty > Connection > Ssh > Tunnels > Source Port 8080, Destination "localhost:80"

accéder au serveur via http://localhost:8080

Redirections locales
....................

::

   ssh -L 2022:remote.edu:22 intdude@intermediate.edu 
   
This creates an "ssh tunnel" starting at localhost:2022 through intermediate.edu (which has the default ssh port of 22) to remote.edu:22.
As a byproduct it gives you a shell on intermediate.edu. The idea is that you can use ssh to connect to remote.edu from localhost through the tunnel. 

::

   M0:$ ssh -L 1234:localhost:80 M1

Effectuera un tunnel de M0:1234 vers M1:80 en passant par M1:22 ("localhost" comme destination sera le localhost du serveur intermédiaire)

::

   M0:$ ssh -L 1234:M1:80 M1 :-/
   
La connexion est identique mais utilisera l'adresse de la M1 (interface réseau ) plutôt que l'interface lo.

::

   M0:$ ssh -L 1234:M0:80 M1

La commande connecte M1 sur M0:80.

::

   M0:$ ssh -L 1234:M2:80 M1
Il y aura une connexion (un tunnel créé) entre M0 et M1 mais la redirection est effectuée entre M1:1234 et M2:80 en utilisant M1:22. 
Les transactions sont chiffrées entre M0 et M1, mais pas entre M1 et M2, sauf si un second tunnel ssh est créé entre M1 et M2.

Redirections distantes
......................

::

   M0:$ ssh -R 1234:HOSTNAME:80 M1

Ici M0 à le serveur TCP, il sert donc de relais entre une connexion M1:1234 et HOSTNAME:80. La connexion est chiffrée entre M1 et M0. 
Le chiffrement entre M0 et HOSTNAME dépend de la liaison mise en place.

::

   M0:$ ssh -R 1234:localhost:80 M1

Cela ouvre une connexion depuis M1:1234 vers M0:80 car localhost correspond, ici, à M0.
Si un utilisateur passe une requête sur M1:1234, elle sera redirigée vers M0:80.

::

   M0:$ ssh -R 1234:M2:80 M1

Cela ouvre une connexion entre M0 et M1:22, mais les requêtes allant de M1:1234 sont redirigés sur M2:80.
Le canal est chiffré entre M1 et M0, mais pas entre M0 et M2.
(voir http://www.linux-france.org/prj/edu/archinet/systeme/ch13s04.html)
option ssh -NfL pour envoyer en background et quitter automatiquement

Redirection avec socat (socket cat) vers un port d'un serveur distant
.....................................................................

socat sert principalement à relayer deux flux de données de manière bidirectionnelle::

   sudo socat tcp-listen:8000,reuseaddr,fork tcp:192.168.1.1:8000

voir http://www.dest-unreach.org/socat/doc/socat.html#EXAMPLES


