Docker
======

Construction d'un container
---------------------------

cd /opt/docker/clamd
docker build -t clamd .

S'attacher au container et rouler bash
--------------------------------------

docker exec -it container /bin/bash

Logs d'un container Docker
--------------------------

docker logs -f container


Pousser l'image docker sur un autre serveur
-------------------------------------------

docker save clamd|ssh qxadweb20.fea.shq.local "docker load"



Reset du network de Docker
-------------------------
Si plus capable de se connecter via SSH à partir de nos postes mais qu'on peut à partir d'un serveur
1) Arrêter les docker qui roulent
docker rm -f ...
2) Clean up du network
docker network ls
3) On enlève les networks qui ont un nom *_default
docker network rm accesdistant_default partenaires_default shq_default
docker prune
4) Redémarrer les docker
docker .. ou docker-compose ...
