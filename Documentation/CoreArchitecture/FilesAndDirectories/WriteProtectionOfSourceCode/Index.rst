

.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. ==================================================
.. DEFINE SOME TEXTROLES
.. --------------------------------------------------
.. role::   underline
.. role::   typoscript(code)
.. role::   ts(typoscript)
   :class:  typoscript
.. role::   php(code)


Write protection of source code
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The source code needs to be writeable at certain points. Lets define
some rules:


Backend / Source code:
""""""""""""""""""""""

- Generally  *you can write protect the whole TYPO3 source code* (that
  is the typo3\_src/\* (more specifically typo3/ and t3lib/) directories
  and their contents)

- ... except: "typo3/ext/" if you wish TYPO3 to install global
  extensions for you.


Frontend (local website):
"""""""""""""""""""""""""

- typo3temp/, uploads/ (+ subdirs) and typo3conf/ (+ subdirs) must be
  writeable.

The ownership of the files should be the webserver user executing the
scripts.

On unix-boxes you can use this command:

::

   chmod 555 typo3_src/ -R

**Notice:** A typical mistake on UNIX systems regarding the write
permissions is if you look at the write permission for eg.
“typo3conf/localconf.php” and see that this file should be writeable.
If TYPO3 tells you that it is not writeable it's most likely because
you didn't allow PHP to write to the typo3conf/  *directory* as well!

