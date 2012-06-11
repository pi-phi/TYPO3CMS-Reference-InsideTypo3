

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


User and Page TSconfig
^^^^^^^^^^^^^^^^^^^^^^

"User TSconfig" and "Page TSconfig" are very flexible concepts for
adding fine-grained configuration of the backend of TYPO3. It is text-
based configuration system where you assign values to keyword-strings
entered in a database table field. The syntax used is TypoScript.
There is a document, `"TSconfig", describing in detail how it works
<../Sites/typo3/doc_core_tsconfig/doc/manual.sxw>`_ and which options
it includes.


User TSconfig
"""""""""""""

User TSconfig can be set for each backend user and group.
Configuration set for backend groups is inherited by the user who is a
member of those groups. The available options typically cover user
settings like those found in the User>Setup module (in fact options
from that module can be forcibly overridden from User TSconfig!),
configuration of the "Admin Panel" (frontend), various backend tweaks
(lock user to IP, show shortcut frame, may user clear all cache?,
width of the navigation frame etc.) and backend module configuration
(overriding any configuration set for backend modules in Page
TSconfig).

You can find more `details about User TSconfig in the "TSconfig"
document <../Sites/typo3/doc_core_tsconfig/doc/manual.sxw#User%20TScon
fig%7Coutline>`_ .


Page TSconfig
"""""""""""""

Page TSconfig can be set for each page in the page tree. Tree branches
inherit configuration for pages closer to the tree root. The available
options typically cover backend module configuration which means that
modules related to page ids (those in the "Web" main module) can be
configured for different behaviours in different branches of the tree.
It also includes configuration of TCEforms and TCEmain including Rich
Text Editor behaviours. Again, the point is that the configuration is
active for certain branches of the page tree which is very practical
in projects running many sites in the same page tree.

You can find more `details about Page TSconfig in the "TSconfig"
document <../Sites/typo3/doc_core_tsconfig/doc/manual.sxw#Page%20TScon
fig%7Coutline>`_ .

