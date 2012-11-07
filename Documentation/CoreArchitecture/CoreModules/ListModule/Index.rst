.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


List module
^^^^^^^^^^^

The list module is like the file manager in an Operating System; it
provides basic access to all "elements" available in the system. In
TYPO3 almost all information is stored in the database and managed
after the same principles internally. For instance Content Elements
representing page content are database records just like backend users
are. The Web>List module allows us to create, modify and delete both
kinds of records after the same principles. However, "context
sensitive" management of Content Elements when building web page
content is better done with specialized modules like the "Page" module
which also provides access to Content Elements but from a CMS
perspective rather than a raw "list perspective".

In this screenshot you can see the list module showing the content of
a page in the page tree. Two tables had records associated by that
page and they are shown in the listing.

|img-137|

Likewise you can use the list module to view the content of the page
tree root (PID=0). The page tree root contains records related to the
whole system (like backend users) and is only editable for backend
users. In this listing you can see the only backend users available in
this system, the "admin" user:

|img-138|

Clicking the icons of the records in the Web>List module will make a
Context Sensitive Menu (CSM) appear over them providing options for
copying, pasting, editing, creating new elements etc. If you enable
the "Extended view" module you will find many of these options
directly in the listing:

|img-139|

Another feature of the Web>List module is that you can view a single
table only by clicking the table header. In the single listing mode
you can add additional fields from the table to be listed. Also notice
how edit icons has appeared over each column in the list. These allow
you to edit a single field (or group of fields) from all listed
records in one screen. Very nice feature.

|img-140|


Page TSconfig options for Web>List module
"""""""""""""""""""""""""""""""""""""""""

You can configure the List module (as well as other backend modules)
for special behaviours depending on which branch in the page tree you
use (or on user basis). Please see the guide `"TSconfig" for the
available options for backend modules
<../Sites/typo3/doc_core_tsconfig/doc/manual.sxw#-%3EMOD%7Coutline>`_
.

