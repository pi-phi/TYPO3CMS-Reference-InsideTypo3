.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


TYPO3 files and folders
^^^^^^^^^^^^^^^^^^^^^^^


The TYPO3 source code-library consists of these folders:
""""""""""""""""""""""""""""""""""""""""""""""""""""""""

If you have downloaded the "typo3src\_[xxx].tgz" version of TYPO3s
source code you will see these directories:

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   folder
         folder

   b


.. container:: table-row

   folder
         t3lib/

   b
         TYPO3 libraries which are mostly for the backend, but some are used by
         the frontend as well. Includes a folder with fonts and graphics.


.. container:: table-row

   folder
         typo3/

   b
         TYPO3 backend administration directory. This has been described in
         detail earlier in this document.


.. container:: table-row

   folder
         misc/

   b
         Supplementary scripts (like superadmin.php) and old changelogs for
         previous versions. Not needed by any online site and can safely be
         removed.


.. ###### END~OF~TABLE ######

**Please notice** that the source code  *itself* will not run out of
the box - it must be set up with local site files to form a proper
website based on TYPO3. See the introduction to this document for more
information and further, seek help in other documents if that is what
you need. Possibly you should download what is called a "package" if
you need an out-of-the-box running website.


Files of typo3/
"""""""""""""""

See the document "TYPO3 Core API" for a list of the source code files.
There you can also see which files might be of interest to you.

