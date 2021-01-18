reStructuredText
================

Réf.: http://openalea.gforge.inria.fr/doc/openalea/doc/_build/html/source/sphinx/rest_syntax.html#
et https://cheat.readthedocs.io/en/latest/rst.html

reStructuredText est un système d'analyse et de syntaxe de balisage en texte clair facile à lire, ce que vous voyez est ce que vous obtenez. Il est utile pour la documentation de programme en ligne (comme les docstrings Python), pour créer rapidement des pages Web simples et pour des documents autonomes.


Avertissement:

   Tout comme Python, la syntaxe reST est sensible à l'indentation!
   reST requiert des lignes vides entre les paragraphes 
   
Usage de base
-------------

Utiliser un astérisque de chaque côté du texte pour le mettre en italique, 2 astuse one asterisk on each side of a text you want to emphasize in italic and 2 asterisks in you want to make it bold::

    *italic*
    **bold**

Les double backquotes sont utilisées pour rendre le texte litéralement. Par exemple, pour utiliser le caractère spécial *::

    Le caractère spécial ``*`` n'est pas interprété

Finallement, un single backquote est utilisé pour les commandes spéciales reST (par exemple, hyperliens avec des espaces)::

    Voici comment créer un hyperlien (voir plus loin)  `OpenAlea wiki <openalea.gforge.inria.fr>`_

Note

    Si l'astérisque ou backquotes apparait dans le texte et pourrait être confondu comme délimiteur markup, il faut le précéder d'un backslash.


Usage avancé
------------
Soyez conscient de certaines restrictions de ce balisage:

    il peut ne pas être imbriqué,
    le contenu peut ne pas commencer ou se terminer par un espace: * le texte * est incorrect,
    il doit être séparé du texte environnant par des caractères autres que des mots.

Utilisez un espace d'échappement avec une barre oblique inverse pour contourner ce problème:

     c'est un paragraphe ``*long\*`` est correct et donne *longish*.
     c'est un paragraphe ``long*ish* n'est pas interprété comme prévu. Vous devriez utiliser ceci est un paragraphe ``long\*ish*`` pour obtenir un paragraphe long\*ish*


Use a backslash escaped space to work around that:

    this is a *longish* paragraph is correct and gives longish.
    this is a long*ish* paragraph is not interpreted as expected. You should use this is a long\*ish* paragraph to obtain longish paragraph


Entêtes
-------

Pour écrire un titre, il faut le souligner::

    ######
    Partie
    ######
    
    ********
    Chapitre
    ********

    Section
    =======
    
    Sous-section
    ------------
    
    Sous-Sous-section
    ^^^^^^^^^^^^^^^^^


Deux règles:

    Utiliser autant de caractères que la longueur du titre
    L'utilisation des caractères est flexible mais doit être consistant

Normalement, aucun niveau de titre n'est attribué à certains caractères car la structure est déterminée à partir de la succession de titres. Cependant, pour la documentation Python, cette convention est utilisée que vous voudrez peut-être suivre:

     # avec overline, pour les pièces
     * avec overline, pour les chapitres
     =, pour les sections
     -, pour les sous-sections
     ^, pour les sous-sous-sections
     ", Pour les paragraphes


Cheatsheets
-----------

Copied from http://docs.sphinxdocs.com/en/latest/cheatsheet.html - thanks
to Read The Docs.

BUGS:

* ``codeblock`` should be ``code-block``

.. image:: sphinx-cheatsheet-front-full.png

.. image:: sphinx-cheatsheet-back-full.png
