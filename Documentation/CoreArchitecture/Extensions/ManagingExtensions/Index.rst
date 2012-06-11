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


Managing extensions
^^^^^^^^^^^^^^^^^^^


Installing extensions
"""""""""""""""""""""

Extensions available to a TYPO3 installation can be installed by the
Extension Manager which is a core module:

|img-26|

Here three extensions are installed and as you can see they are
apparently adding backend modules to the menu. Basically installing
/de-installing an extension is a matter of clicking the +/- button
next to the extension. In some cases additional accept of for example
database tables/field additions are necessary but the process itself
is as simple as that!


Importing extensions
""""""""""""""""""""

If an extension is not available on the server you can import it from
the TYPO3 Extension Repository (TER) or manually upload it from a file
(if you have a T3X file available):

|img-27|

Connecting to the online repository will show a list like this:

|img-28|

You can easily see which extensions are not locally available on your
server and with a single click on the import icon the extension is
downloaded from the repository and installed on your server!

Bottom-line is: In less than 30 seconds you can import and install an
extensions with all database tables and fields automatically created
for you, ready for use!


More about extensions?
""""""""""""""""""""""

This was just a short introduction so you could grasp the potential of
extensions. Since this document is about the TYPO3 core you can read
more about the `Extension API in the document "TYPO3 Core API"
<#TYPO3%20Extension%20API%7Coutline>`_ . You can also find tutorials
about `extension programming on TYPO3.org <http://typo3.org/>`_ . If
you wish to investigate publicly available extensions go to `typo3.org
<http://typo3.org/1420.0.html>`_ where the TYPO3 Extensions Repository
has a frontend for just that:

|img-29|

