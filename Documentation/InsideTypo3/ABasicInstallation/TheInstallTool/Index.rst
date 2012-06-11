.. include:: Images.txt

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


The Install Tool
^^^^^^^^^^^^^^^^

So we go to "coreinstall/typo3/install/index.php" but see this
message:

::

   In the main source distribution of Typo3, the install script is disabled by a die() function call.
   Open the file typo3/install/index.php and remove/out-comment the line that outputs this message!

After having removed the die() function call in the file
.../install/index.php file we can enter the Install Tool (password was
"joh316" by default). Then go to the "Basic Configuration" menu item.


Creating a database
"""""""""""""""""""

Go to the bottom of the page and enter a database name:

|img-6|


Creating required tables
""""""""""""""""""""""""

Then go to the "Database Analyzer":

|img-7|

OK, so we are connected, we have a database. But zero tables. Kein
problem:

|img-8|

First "Update required tables" (Click #1 and click "Write to
database"),

then "Dump static data" (Click #2, tick off "Import the whole file..."
and "Write to database"), then create an "admin" user so you can login
(Click #3, enter username/password and accept).

***Notice:***  *With a core-only install of TYPO3 there is currently
no static table data so this step can be skipped. However it's
included here for the completeness.*

Now you can go to the typo3/ directory again and you will have a login
box:

If you login you will see this:

|img-9|


Checking other requirements
"""""""""""""""""""""""""""

Finally we will revisit the "Basic Configuration" menu item and check
if the rest of the requirements are met:

|img-10|

We find that this is not the case with particularly two directories:
uploads/ and typo3temp/. There are a number of other missing
directories which issues a warning, but that is because those are
typically used with the "cms" extension frontend. That is disabled
now. Remember? - Core only!

So

::

   # mkdir typo3temp/
   # mkdir uploads/

... and all is fine.

