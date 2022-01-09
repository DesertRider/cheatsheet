UFW / firewalld
===============

UFW
---

Commandes générales
~~~~~~~~~~~~~~~~~~~

Activer le firewall::

   ufw enable
   
Désactiver le firewall::

   ufw disable

Statut du firewall::

   ufw status

Lister les filtres ajoutés::

   ufw show added


Permettre des accès
~~~~~~~~~~~~~~~~~~~

Permettre un port sur protocole::

   ufw allow PORT[/PROTOCOLE]
   ufw allow 22/tcp

Permettre un service (utilise /etc/services)::

   ufw allow ssh

Permet l'accès complet à partir d'une adresse IP::

   ufw allow from 192.168.2.100

Permet l'accès à un port pour une adresse IP::

   ufw allow from TARGET to DESTINATION port PORTNUMBER [proto PROTOCOL]
   ufw allow from 192.168.2.100 to any port 22 proto tcp

Bloquer (refuser) des accès
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Refuser l'accès à un port::

   ufw deny POPRT[/PROTOCOLE]
   ufw deny 3306/udp

Refuser un service::

   ufw deny ftp

Refuser l'accès depuis une adresse IP::

   ufw deny from 192.168.2.99

Refuser l'accès à un port spécifique depuis une adresse IP::

   ufw deny from IPADDRESS to PROTOCOL port PORTNUMBER
   ufw deny from 192.168.2.99 to any port 80

Limiter les connexions à un port
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you limit a connection, UFW will not allow any more than six connections within the last 30 seconds. The firewall will block any additional connections.
::

   ufw limit PORT[/PROTOCOL]
   ufw limit 22

Retirer des règles
~~~~~~~~~~~~~~~~~~

Retirer une règle::

   ufw delete RULE
   ufw delete limit 22/tcp
   
Retirer une règle d'après son numéro de règle::

    ufw status numbered
    ufw delete RULENUMBER

FIREWALL-CMD
------------

Commandes générales
~~~~~~~~~~~~~~~~~~~

Activer firewalld::

   systemctl enable firewalld
   
Redémarrer firewalld::

   systemctl restart firewalld
   
Lister les services et ports filtrés::

   firewall-cmd --list-services
   firewall-cmd --list-ports
   
Zones
~~~~~

Lister et voir la zone active::

   firewall-cmd --list-all-zones
   firewall-cmd --get-default-zone
   
   
Ajout de règles
~~~~~~~~~~~~~~~

Ajout d'une règle pas permanente (mise en place immédiate)::

   firewall-cmd --add-port=[YOUR PORT]/tcp
   
Ajout d'une règle permanente (activé à la réactivation de firewalld)::

   firewall-cmd --permanent --add-port=[YOUR PORT]/tcp
