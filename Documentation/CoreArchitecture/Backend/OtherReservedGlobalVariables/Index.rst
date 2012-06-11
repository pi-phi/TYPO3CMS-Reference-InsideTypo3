

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


Other reserved global variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In addition to the global variables declared in "init.php" there are a
number of other reserved global variables which has a recognized
importance. These are always defined outside "init.php" either prior
to or after the inclusion of "init.php".

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Global variable
         Global variable
   
   Defined in
         Defined in
   
   Description
         Description
   
   Avail. in FE
         Avail. in FE


.. container:: table-row

   Global variable
         *$MLANG*
   
   Defined in
         [prior to init.php / conf.php of modules]
   
   Description
         Contains a limited amount of language labels: The title, icon and
         description of the module.
   
   Avail. in FE
         -


.. container:: table-row

   Global variable
         *$MCONF*
   
   Defined in
         [prior to init.php / conf.php of modules]
   
   Description
         Contains a few module-cofiguration informations like the name, access
         and which script to use. Primarily used by access control and the
         class t3lib\_loadmodules.
   
   Avail. in FE
         -


.. container:: table-row

   Global variable
         *$BACK\_PATH*
   
   Defined in
         [prior to init.php / conf.php of modules]
   
   Description
         Possibly set in the parent script including "init.php" pointing back
         to the "TYPO3\_mainDir" from wherever the parent script is located.
         Used primarily for images and links. See discussion on
         "TYPO3\_MOD\_PATH" and modules in general.
   
   Avail. in FE
         -


.. container:: table-row

   Global variable
         *$LOCKED\_RECORDS*
   
   Defined in
         t3lib\_BEfunc
   
   Description
         Locking of records is cached in this variable.
   
   Avail. in FE


.. ###### END~OF~TABLE ######

