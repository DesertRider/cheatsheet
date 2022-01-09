Commandes reliées au firewall du serveur
========================================

UFW
---

Activer le firewall::

ufw enable

Statut du firewall::

ufw status

Lister les filtres ajoutés::

ufw show added

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

Refuser l'accès à un port::

ufw deny POPRT[/PROTOCOLE]
ufw deny 3306/udp

Refuser un service::

ufw deny ftp

Refuser l'accès depuis une adresse IP:

ufw deny from 192.168.2.99

Refuser l'accès à un port spécifique depuis une adresse IP::

ufw deny from IPADDRESS to PROTOCOL port PORTNUMBER
ufw deny from 192.168.2.99 to any port 80

Limiter les connexions à un port::

ufw limit PORT[/PROTOCOL]
ufw limit 22

FIREWALL-CMD
------------
