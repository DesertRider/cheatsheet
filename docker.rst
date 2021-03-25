Docker
======

Terminology
...........

Container: A container is used to execute an image.  See ``docker run``,
``docker-compose up``.

Image: A kind of snapshot of a computer system that can be run in a container.
Images are built from Dockerfiles.  See ``docker build``, ``docker-compose build``.

Common commands
...............

Build an image from Dockerfile in current directory::

   docker build -t imagetag .

Start a container from an image, run a command, and when the
command exits, stop the container without saving any changes::

   docker run --rm -it imagetag bash
   
Démarrer un container et le laisser s'exécuter en background, remapper port 22 sur 2222::

   docker run -it -d -p 2222:22 ubuntu-with-sshd

Cleanup
.......

remove docker containers
------------------------

see: http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images

.. codeblock: python
   :linenos:
   :emphasize-lines: 2

   $ docker ps
   $ docker ps -a
   $ docker rm $(docker ps -qa --no-trunc --filter "status=exited")

remove docker images
--------------------

see: http://stackoverflow.com/questions/32723111/how-to-remove-old-and-unused-docker-images

::

    $ docker images
    $ docker rmi $(docker images --filter "dangling=true" -q --no-trunc)

    $ docker images | grep "none"
    $ docker rmi $(docker images | grep "none" | awk '/ / { print $3 }')
    
.. csv-table:: docker-image-table
   :header: "Command", "Description"
   :widths: 15, 15

    "docker image build", "Build an image from a Dockerfile"
    "docker image history", "Show the history of an image"
    "docker image import", "Import the contents from a tarball to create a filesystem image"
    "docker image inspect", "Display detailed information on one or more images"
    "docker image load", "Load an image from a tar archive or STDIN"
    "docker image ls", "List images"
    "docker image prune", "Remove unused images"
    "docker image pull", "Pull an image or a repository from a registry"
    "docker image push", "Push an image or a repository to a registry"
    "docker image rm", "Remove one or more images"
    "docker image save", "Save one or more images to a tar archive (streamed to STDOUT by default)"
    "docker image tag", "Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE"

delete volumes
--------------

see: https://github.com/chadoe/docker-cleanup-volumes

::

    $ docker volume rm $(docker volume ls -qf dangling=true)
    $ docker volume ls -qf dangling=true | xargs -r docker volume rm

delete networks
---------------

::

    $ docker network ls
    $ docker network ls | grep "bridge"
    $ docker network rm $(docker network ls | grep "bridge" | awk '/ / { print $1 }')

Resize disk space for docker vm
-------------------------------

::

    $ docker-machine create --driver virtualbox --virtualbox-disk-size "40000" default



Construction d'un container
---------------------------

::

   cd /opt/docker/clamd
   docker build -t clamd .

S'attacher au container et rouler bash
--------------------------------------

::

   docker exec -it container /bin/bash

Logs d'un container Docker
--------------------------

::

   docker logs -f container


Pousser l'image docker sur un autre serveur
-------------------------------------------

::

   docker save clamd|ssh qxadweb20.fea.shq.local "docker load"

Reset du network de Docker
--------------------------
Si plus capable de se connecter via SSH à partir de nos postes mais qu'on peut à partir d'un serveur

Arrêter les docker qui roulent::

   docker rm -f ...

Clean up du network::

   docker network ls

On enlève les networks qui ont un nom *_default::

   docker network rm accesdistant_default partenaires_default shq_default
   docker network prune

Redémarrer les docker::

   docker .. ou docker-compose ...

