.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


The Backend Adminstration Directory, "typo3/"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the directory "coreinstall/" I create a symlink to the typo3/
administration directory::

   # ln -s ../typo3_src/typo3/

The lets see what happens if I point my web browser at this directory:

|img-4|

Yes of course - the configuration directory. "typo3conf/" is a
*local* directory which contains  *site specific* files. That can be
locally installed extensions, special scripts, special all kinds of
things and of course the obligatory "localconf.php" file! In other
words: The "typo3conf/" folder of a TYPO3 installation contains
*local, unique files* for the website while the "typo3/" folder (along
with others) contains  *general source code* that could have been
shared between all installations on a server. Well, read more about
this in the :ref:`Installation and Upgrade Guide
<t3install:in-depth-installation>` .

