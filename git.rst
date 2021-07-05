Git
===

Workflow
--------

.. image:: https://miro.medium.com/max/481/0*psCSE-BxW3zn4Ya1.png
      :width: 200pt


Commandes principales
---------------------

:Configuration:

   Configurer le nom de l'utilisateur::
     
      git config --global user.name "My name"
         
   Configurer l'adresse de courriel::
      
      git config --global user.email "my.email@domain.com"
         
   Sauvegarder les crédentiels pour le repo distant::
      
      git config credential.helper store
         
   Ignore les problèmes de certificats::
      
      git config --global http.sslVerify false
         
   Configure le proxy à utiliser::
      
      git config --global https.proxy https://httpproxy:3128
      git config --global http.proxy http://httpproxy:3128

   Lister les éléments de la configuration en fonction::
   
      git config -l
      
      
:Initialisation:
   
   Initialise un répertoire pour suivi de version::
      
      git init
         
   Cloner un repo existant::
      
      git clone https://github.com/DesertRider/cheatsheet.git
      git clone ssh://user@site.com/directory/repository.git
         
:Changements:
   
   Ajouter un fichier ou répertoire au suivi de version::
      
      git add répertoire/fichier
      
   Retirer le fichier de ceux ajouté par git add::
   
      git restore --staged fichier
      
   Enlever un changement (pas le fichier, le changement prévu au repo)::
   
      git rm fichier
         
   Voir les modifications récentes::
      
      git log [fichier] [--pretty=one-line]
      
         
   Voir ce qui a changé pour un fichier depuis une certaine version::
      
      git diff
         
   Affiche les changements en attente d'un commit::
      
      git status
      
   Pousse les changements dans le repo local::
      
      git commit [ -m message ]
         
   Pousse les changements commits dans le repo distant::
      
      git push
         
   Récupère les changements qui sont dans le repo distant::
      
      git pull
      
   Ignorer des répertoires/fichiers::
   
      créer un fichier .gitignore et lister les éléments à ignorer
    
:Remote repository:

   Afficher les informations sur les remote repositories utilisés::
   
      git remote -v
      
   
      


3 cas d'initialisation d'un repo
--------------------------------

:Create a new repository:

   ::
   
      git clone https://site.com/directory/myrepo.git
      cd myrepo
      touch README.md
      git add README.md
      git commit -m "add README"
      git push -u origin master

:Existing folder:

   ::

      cd existing_folder
      git init
      git remote add origin https://site.com/directory/myrepo,git
      git add .
      git commit -m "Initial commit"
      git push -u origin master

:Existing Git repository:

   ::
   
      cd existing_repo
      git remote rename origin old-origin
      git remote add origin https://site.com/directory/myrepo.git
      git push -u origin --all
      git push -u origin --tags


Personnalisation du message lors du commit
------------------------------------------
::

    cat > ~/.gitmessage <<FIN
    # |<--- Résumez le changement en 50 car. max --->|
    
    # Sautez une ligne et décrivez le pourquoi et non le comment du changement
    # |<---- Essayez de vous limiter vos lignes à 72 caractères max!  ---->|

    # Vous pouvez ajouter d'autres paragraphes, par exemple une référence
    # au billet qui signale le problème, ...
    FIN

    git config --global commit.template ~/.gitmessage
