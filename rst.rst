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


Section de Dan Poirier
----------------------


REST reStructuredText notes
(see also Sphinx notes)

SEE CHEATSHEET AT END

* `rst tutorial <http://sphinx-doc.org/tutorial.html>`_
* `rst primer <http://sphinx-doc.org/rest.html#rst-primer>`_
* `rst markup <http://sphinx-doc.org/markup/index.html#sphinxmarkup>`_
* `autodoc <http://sphinx-doc.org/ext/autodoc.html?highlight=autodoc#sphinx.ext.autodoc>`_

Example::

    file1.rst
    ---------

    Contents:

    .. toctree::
       :maxdepth: 2

       keys
       api


    Go read :ref:`morestuff` for more.  Read about python package :py:mod:`package.name`
    and python function :py:func:`package.name.function`.  The python class
    :py:class:`package.name.ClassName` might also be useful, and its method
    :py:meth:`package.name.ClassName.method`.  Not to mention the attribute
    :py:attr:`package.name.ClassName.attrname`.  The code might throw the exception
    :py:exc:`package.name.MyException`.

    file2.rst
    ---------

    .. _morestuff:

    More stuff
    ==========

    To show code::

        Indent this 4 spaces.
           You can indent more or less.
        And keep going.

        Even include blank lines

    It ends after a blank line and returning to the original indentation.

    You can also markup ``short inline code`` like this.

Automatically include the doc for a class like this::

    .. _api:

    .. autoclass:: healthvaultlib.healthvault.HealthVaultConn
        :members:

And document them::

    class MyClassName(object):
       """
       Description.  Can refer to :py:meth:`.method1` here or anywhere in the file.

       :param string parm1: His name
       :param long parm2: His number
       """

       def __init__(self, parm1, parm2):
          pass

       def method1(self, arg1, arg2):
          """
          Description

          :param unicode arg1: something
          :param object arg2: something else
          """

http://techblog.ironfroggy.com/2012/06/how-to-use-sphinx-autodoc-on.html

Various code blocks::

    .. code-block:: bash|python|text
       :linenos:
       :emphasize-lines: 1,3-5

       # Hi
       # there
       # all
       # you
       # coders
       # rejoice

.. code-block:: bash
    :linenos:
    :emphasize-lines: 1,3-5

    # Hi
    # there
    # all
    # you
    # coders
    # rejoice


You can include an ```HTML link`_`` like this
and the definition can go nearby or at the bottom of the page::

    .. _HTML link: http://foo.bar.com/

Or you can just write ```HTML link <http://foo.bar.com>`_``
all in one place.

http://sphinx-doc.org/markup/inline.html#ref-role

Link to a filename in this set of docs using ``:doc:`Any text you want </path/to/page>```
or just ``:doc:`path```.

Don't include the ".rst" on the end of the filename. Relative filenames
work too. But it's better to use :ref:, see next.

You can define an anchor point, which Sphinx calls
a label. Put this above a section header::

    .. _my-label:

    My Section
    ----------

Now from somewhere else, you can write ``:ref:`my-label```
and it'll be rendered as "My Section" and will link to the
section.  If you want some other text in the link, you
can write ``:ref:`any text <my-label>``` instead.

Cheatsheets
-----------

Copied from http://docs.sphinxdocs.com/en/latest/cheatsheet.html - thanks
to Read The Docs.

BUGS:

* ``codeblock`` should be ``code-block``

.. image:: sphinx-cheatsheet-front-full.png

.. image:: sphinx-cheatsheet-back-full.png
