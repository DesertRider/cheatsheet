reStructuredText
================

Réf.: http://openalea.gforge.inria.fr/doc/openalea/doc/_build/html/source/sphinx/rest_syntax.html#
et https://cheat.readthedocs.io/en/latest/rst.html

reStructuredText is an easy-to-read, what-you-see-is-what-you-get plaintext markup syntax and parser system. It is useful for in-line program documentation (such as Python docstrings), for quickly creating simple web pages, and for standalone documents.

basic usage:	

    use one asterisk on each side of a text you want to emphasize in italic and 2 asterisks in you want to make it bold:

    *italic*
    **bold**

    double backquotes are used to make a text verbatim. For instance, it you want to use special characters such as *:

    This ``*`` character is not interpreted

    Finally, the single backquote is used for reST special commands (e.g., hyper links with spaces):

    This is how to create hyperlinks (see later)  `OpenAlea wiki <openalea.gforge.inria.fr>`_

    Note

    If asterisks or backquotes appear in running text and could be confused with inline markup delimiters, they have to be escaped with a backslash.

advanced usage:	

Be aware of some restrictions of this markup:

    it may not be nested,
    content may not start or end with whitespace: * text* is wrong,
    it must be separated from surrounding text by non-word characters.

Use a backslash escaped space to work around that:

    this is a *longish* paragraph is correct and gives longish.
    this is a long*ish* paragraph is not interpreted as expected. You should use this is a long\ *ish* paragraph to obtain longish paragraph



Section de Dan Poirier
======================


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
