Git
===

Commandes principales
---------------------
   
.. csv-table:: 
   :header: "Commandes", "Description"
   :widths: 15, 30

    "git config --global user.name My name", "Configure le nom de l'utilisateur"
    "git config --global user.email my.email@domain.com", "Configure l'adresse de courriel"
    "git config credential.helper store", "permet de sauvegarder les crédentiels pour repo distant"
    "git config --global http.sslVerify false", "ignore les problèmes de certificats"
    "git init", "initialiser un répertoire pour avoir un repo"
    "git clone https://github.com/DesertRider/cheatsheet.git", "Cloner repo (http/s, ssh)"
    "git add fichier/répertoire", "ajouter un fichier au suivi de version"
    "git log", "voir les modifications récentes"
    "git diff", "voir ce qui a changé pour un fichier depuis une certaine version"
    "git revert", "annule une unique modification"
    "git status", "affiche les changements en attente d'un commit"
    "git commit [-m message]", "pousse les changements dans le repo local, avec en option le message de commit"
    "git push", "pousse les changements commits dans le repo distant"  
    "git pull", "récupère les changements qui sont dans le repo distant"

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
