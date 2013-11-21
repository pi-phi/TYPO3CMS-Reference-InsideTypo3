.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Global variables, Constants and Classes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After init.php has been included there is a set of variables,
constants and classes available to the parent script. In the document
"TYPO3 Core API" you can see `two tables listing these constants and
variables <#Variables%20and%20Constants%7Coutline>`_ .

The column "Avail. in FE" is an indicator that tells you if the
constant, variable or class mentioned is also available to scripts
running under the frontend of the "cms" extension. Strictly this is
not a part of the core (which is what we deal with in this document),
but since the "cms" extension is practically always a part of a TYPO3
setup it's included here as a service to you.


Classes
"""""""

This is the classes already included after having included "init.php":

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Class
         Class

   Included in
         Included in

   Description
         Description

   Avail. in FE
         Avail. in FE


.. container:: table-row

   Class
         t3lib\_div

   Included in
         init.php

   Description


   Avail. in FE
         YES


.. container:: table-row

   Class
         t3lib\_extMgm

   Included in
         init.php

   Description


   Avail. in FE
         YES


.. container:: table-row

   Class
         t3lib\_db

   Included in
         init.php

   Description


   Avail. in FE
         YES


.. container:: table-row

   Class
         t3lib\_userauth

   Included in
         init.php

   Description


   Avail. in FE
         YES


.. container:: table-row

   Class
         t3lib\_userauthgroup

   Included in
         init.php

   Description


   Avail. in FE
         -


.. container:: table-row

   Class
         t3lib\_beuserauth

   Included in
         init.php

   Description


   Avail. in FE
         -


.. container:: table-row

   Class
         t3lib\_iconworks

   Included in
         init.php

   Description


   Avail. in FE
         -


.. container:: table-row

   Class
         t3lib\_befunc

   Included in
         init.php

   Description


   Avail. in FE
         -


.. container:: table-row

   Class
         t3lib\_cs

   Included in
         init.php

   Description


   Avail. in FE
         YES


.. container:: table-row

   Class
         *gzip\_encode*

   Included in
         init.php

   Description
         Output compression class by Sandy McArthur, Jr. Included if option is
         set in TYPO3\_CONF\_VARS.

   Avail. in FE
         (YES)


.. ###### END~OF~TABLE ######

Possibly other classes could have been included in "ext\_tables.php"
files or "ext\_localconf.php" files. This is OK for the
"localconf.php" file, but not necessarily for extensions. Please see
the Extension API description for guidelines on this.


System/PHP Variables
""""""""""""""""""""

A short notice on system variables:

Don't use any system-global vars, except these::

   HTTP_GET_VARS, HTTP_POST_VARS, HTTP_COOKIE_VARS

Any other variables may not be accessible if php.ini-optimized is
used!

**Environment / Server variables** are also very critical! Since
different servers and platforms offer different values in the
environment and server variables, TYPO3 features an abstraction
function you should always use if you need to get the REQUEST\_URI,
HTTP\_HOST or something like that. At least never use the PHP function
"getenv()" or take the values directly from HTTP\_SERVER\_VARS -
rather call t3lib\_div::getIndpEnv(" *name\_of\_sys\_variable* ") to
get the value (if it is supported by that function). You can rely on
that function will deliver a consistent value independently of the
server OS and webserver software.

You should refer to the :ref:`TYPO3 Coding Guidelines
<t3cgl:start>` or :ref:`TYPO3 Core API
<t3api:high-priority-functions>` for
more information about this or go directly to the source of
class.t3lib\_div.php.

