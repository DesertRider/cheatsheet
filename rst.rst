****************
reStructuredText
****************

Réf.: http://openalea.gforge.inria.fr/doc/openalea/doc/_build/html/source/sphinx/rest_syntax.html#
et https://cheat.readthedocs.io/en/latest/rst.html

reStructuredText est un système d'analyse et de syntaxe de balisage en texte clair facile à lire, ce que vous voyez est ce que vous obtenez. Il est utile pour la documentation de programme en ligne (comme les docstrings Python), pour créer rapidement des pages Web simples et pour des documents autonomes.


.. warning:: Avertissement!

   Tout comme Python, la syntaxe reST est sensible à l'indentation!
   reST requiert des lignes vides entre les paragraphes 
   
Usage de base
=============

Utiliser un astérisque de chaque côté du texte pour le mettre en italique, 2 astuse one asterisk on each side of a text you want to emphasize in italic and 2 asterisks in you want to make it bold::

    *italic*
    **bold**

Les double backquotes sont utilisées pour rendre le texte litéralement. Par exemple, pour utiliser le caractère spécial *::

    Le caractère spécial ``*`` n'est pas interprété

Finallement, un single backquote est utilisé pour les commandes spéciales reST (par exemple, hyperliens avec des espaces)::

    Voici comment créer un hyperlien (voir plus loin)  `OpenAlea wiki <openalea.gforge.inria.fr>`_

.. note::     Si l'astérisque ou backquotes apparait dans le texte et pourrait être confondu comme délimiteur markup, il faut le précéder d'un backslash.


Usage avancé
============

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
=======

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

Normalement, aucun niveau de titre n'est attribué à certains caractères car la structure est déterminée à partir de la succession de titres. Cependant, pour la documentation Python, cette convention est utilisée que vous voudrez peut-être suivre::

     # avec overline, pour les pièces
     * avec overline, pour les chapitres
     =, pour les sections
     -, pour les sous-sections
     ^, pour les sous-sous-sections
     ", Pour les paragraphes


Directives
==========

reST est basé principalement sur des *directives* définies comme suit::

    .. <nom>:: <arguments>
        :<option>: <valeur>
        
        contenu

exemple::

    .. image:: ../images/test.png
        :width: 200pt
        
Notez l'espace entre la directive et son argument ainsi que la ligne vide entre l'option et le contenu

Liens internes et externes
==========================

:Hyperliens internes:

    All titles are considered as internal hyperlinks that may be refered to using this syntax::

        `Internal and External links`_

    You may also create hyperlink as follows::

        .. _begin:

    And then inserting ``begin_`` in your text. For instance, jump to the beginning of this document rst_tutorial_  

    .. note:: Note the underscore at the end ot the links

:Hyperliens external:

    In order to link to external links simply use::

        `Python <http://www.python.org/>`_

    that is rendered as a normal hyperlink `Python <http://www.python.org/>`_. 


.. note:: If you have an underscore within the label/name, you got to escape it with a '\\' character.


Listes et puces
===============

The following code::

    * This is a bulleted list.
    * It has two items, the second
      item uses two lines. (note the indentation)

    1. This is a numbered list.
    2. It has two items too.

    #. This is a numbered list.
    #. It has two items too.

gives:

* This is a bulleted list.
* It has two items, the second
  item uses two lines. (note the indentation)

1. This is a numbered list.
2. It has two items too.

#. This is a numbered list.
#. It has two items too.

.. note:: if two lists are separated by a blank line only, then the two lists are not differentiated as you can see above.

Tables
======

There are several ways to write tables. Use standard reStructuredText tables as explained here. They work fine in HTML output, however, there are some gotchas when using tables for LaTeX output.

:simple table:

    Simple tables can be written as follows::

        +---------+---------+-----------+
        | 1       |  2      |  3        |
        +---------+---------+-----------+

    which gives:

    +---------+---------+-----------+
    | 1       | 2       | 3         |
    +---------+---------+-----------+



:complex table:

    ::

        +------------+------------+-----------+
        | Header 1   | Header 2   | Header 3  |
        +============+============+===========+
        | body row 1 | column 2   | column 3  |
        +------------+------------+-----------+
        | body row 2 | Cells may span columns.|
        +------------+------------+-----------+
        | body row 3 | Cells may  | - Cells   |
        +------------+ span rows. | - contain |
        | body row 4 |            | - blocks. |
        +------------+------------+-----------+

    gives:

    .. htmlonly::

        +------------+------------+-----------+
        | Header 1   | Header 2   | Header 3  |
        +============+============+===========+
        | body row 1 | column 2   | column 3  |
        +------------+------------+-----------+
        | body row 2 | Cells may span columns.|
        +------------+------------+-----------+
        | body row 3 | Cells may  | - Cells   |
        +------------+ span rows. | - contain |
        | body row 4 |            | - blocks. |
        +------------+------------+-----------+

:another way:

    ::

        =====  =====  ======
           Inputs     Output
        ------------  ------
          A      B    A or B
        =====  =====  ======
        False  False  False
        True   False  True
        =====  =====  ======

    gives:

    .. htmlonly::

        =====  =====  ======
           Inputs     Output
        ------------  ------
          A      B    A or B
        =====  =====  ======
        False  False  False
        True   False  True
        =====  =====  ======

.. note:: table and latex documents are not yet compatible in sphinx, and you should therefore precede them with the a special directive (.. htmlonly::)


The previous examples work fine in HTML output, however there are some gotchas when using tables in LaTeX: the column width is hard to determine correctly automatically. For this reason, the following directive exists::

    .. tabularcolumns:: column spec

This directive gives a â€œcolumn specâ€ for the next table occurring in the source file. It can have values like::

    |l|l|l|

which means three left-adjusted (LaTeX syntax). By default, Sphinx uses a table layout with L for every column. This code::

    .. tabularcolumns:: |l|c|p{5cm}|

    +--------------+---+-----------+
    |  simple text | 2 | 3         |
    +--------------+---+-----------+

gives 

.. htmlonly::

    .. tabularcolumns:: |l|c|p{5cm}|

    +--------------+------------+-----------+
    | title        |            |           |
    +==============+============+===========+
    |  simple text | 2          | 3         |
    +--------------+------------+-----------+


Include other reST files and TOC
================================

Since reST does not have facilities to interconnect several documents, or split
documents into multiple output files, Sphinx uses a custom directive to add 
relations between the single files the documentation is made of, as well as 
tables of contents. The toctree directive is the central element. 

.. code-block:: rest

    .. toctree::
        :maxdepth: 2

        intro
        chapter1
        chapter2

Globbing can be used by adding the *glob* option:

.. code-block:: rest

    .. toctree::
        :glob:

        intro*
        recipe/*
        *

The name of the file is used to create the title in the TOC. You may want to change this behaviour by changing the toctree as follows:

.. code-block:: rest
       
    .. toctree::
        :glob:
       
        intro
        Chapter1 description <chapter1>

Comments and aliases
====================

:Comments: comments can be made by adding two dots at the beginning of a line as follows::

    .. comments

:Aliases:


    The first method is to add at end of your reST document something like::

        .. _Python: http://www.python.org/

    Then, write your text inserting the keywrod ``Python_`` . The final result will be as follows: Python_ . 

    A second method is as follows::

        .. |longtext| replace:: this is a very very long text to include

    and then insert  `|longtext|` wherever needed.
 
    .. note::
        Note that when you define the reference or alias, the underscore is before the keyword. However, when you refer to it, the underscore is at the end. The underscore after the keyword is also used for internal references, citations, aliases ... 



##################
Special directives
##################

colored boxes: note, seealso, todo and warnings
=================================================

There are simple directives like **seealso** that creates nice colored boxes:

.. seealso:: This is a simple **seealso** note. 

created using::

    .. seealso:: This is a simple **seealso** note. Other inline directive may be included (e.g., math :math:`\alpha`) but not al of them.

You have also the **note** and **warning** directives:

.. note::  This is a **note** box.

.. warning:: note the space between the directive and the text

.. todo:: a todo box


Cheatsheets
===========

Copied from http://docs.sphinxdocs.com/en/latest/cheatsheet.html - thanks
to Read The Docs.

BUGS:

* ``codeblock`` should be ``code-block``

.. image:: sphinx-cheatsheet-front-full.png

.. image:: sphinx-cheatsheet-back-full.png
