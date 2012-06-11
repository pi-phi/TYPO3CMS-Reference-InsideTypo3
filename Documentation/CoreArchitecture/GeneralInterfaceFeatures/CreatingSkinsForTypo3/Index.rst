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


Creating skins for TYPO3
^^^^^^^^^^^^^^^^^^^^^^^^

With TYPO3 3.6.0 it is possible to create skins for TYPO3 which will
affect not only the CSS styles used in the backend but also provide
alternatives for all icons in the interface. The result is an
interface with a totally different look but maintaining the same
structure:

|img-155|

This screenshot is from the skin extension “skin360” which is an
example of how skins can be made. The “skin360” extension is therefore
a good place to start to look if you want to create your own skins.


Skinning API
""""""""""""

In “TYPO3 Core API” you can find a section which documents the `API
for TYPO3 skins <#Skinning%20API%7Coutline>`_ . Use this section in
conjunction with example extensions like “skin360”.


IMPORTANT: Skinning and copyrights
""""""""""""""""""""""""""""""""""

Skins make it possible to personalize TYPO3 for your own purposes. For
instance you can insert a customers logo or your own companys logo and
style. However it is very important that you do not go so far that you
effectively rebrand TYPO3!

Rebranding TYPO3 is illegal (by default copyright and trademark laws,
see `details here <http://typo3.org/1310.0.html>`_ ). Rebranding means
that you give the TYPO3 CMS "another name", presumably to sell “your
product” to a customer. So  *never* try to brand TYPO3 as if it was
your own product to which you have the copyright. Always make sure
your custom is aware that they get TYPO3 which is free under the GPL
license.

But how far can you go then? Well, with skinning you can actually
change all graphics of the application, including the login screen
logo and logo in the top left corner of the backend. As long as these
logos do not give the impression that the CMS is something else than
TYPO3 you can personalize these logos as much as you like. You can
name them after the company to which you sell the solution so it feels
personal for them. Or you could mix TYPO3s logo with your companys
logo, stating something like “My Company proudly uses TYPO3 blablabla”
or whatever.

The main reason why you can change these logos is that the official
TYPO3 logo and name is included in the copyright notice of the login
screen and “About Modules” screen. This notice must  *never* be
changed by you and must display "as is". This is what ultimately
identifies to the user that the underlying CMS is in fact TYPO3, not
something else.

On this screenshot below you can see it in effect: The top logo (#1)
could be the one of your company or customer, adding a personal touch
to the login screen. In the bottom (#2) you will see the TYPO3 logo
and product name in the copyright notice. This must not be changed.

|img-156|

Notice, that the bottom message (#2) is not something we have made up
ourselves but required by the GPL license according to this part of
the license:

::

   ...
   If the program is interactive, make it output a short notice like this
   when it starts in an interactive mode:
   
       Gnomovision version 69, Copyright (C) year name of author
       Gnomovision comes with ABSOLUTELY NO WARRANTY; for details type `show w'.
       This is free software, and you are welcome to redistribute it
       under certain conditions; type `show c' for details.
   ...

(The GPL license can be found in the file “GPL.txt” inside the TYPO3
source code)

