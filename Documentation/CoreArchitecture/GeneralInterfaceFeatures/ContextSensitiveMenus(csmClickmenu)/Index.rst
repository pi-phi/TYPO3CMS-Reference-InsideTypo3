.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Context Sensitive Menus (CSM / "Clickmenu")
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

TYPO3 implements a well known principle for accessing options for
elements (database records / files) in the interface; the Context
Sensitive Menu. When users click an icon of a database record or a
file in most TYPO3 backend modules they can access options for the
element in a layer that pops up:

|img-145|

**Notice:** Users have to  *left-click* (normal click) the elements
rather than  *right-click* than they can do in normal GUI
applications. This is due to browser limitations that we have not been
able to overcome yet.


Configuration options in User TSconfig
""""""""""""""""""""""""""""""""""""""

User TSconfig offers configuration options for the menu. Here are some
examples::

   options.contextMenu.options.leftIcons = 1

If set, the icons in the clickmenu appear to the left instead of
right. ::

   options.contextMenu.pageTree.disableItems = view, edit

This would disable the "Show" and "Edit" items in the CSM when showed
in the page tree.

There are :ref:`more options described in the document "TSconfig"
<t3tsconfig:useroptions>` .


Technical details
"""""""""""""""""

The CSM is displayed as a DHTML layer made by a <div> block. Scripts
that implement CSM for any element has to output two blank <div>
blocks with certain id values (contentMenu0/1) inside their HTML body.
They provide a placeholder for level 1 and 2 of the CSM.

The <div> blocks are empty by default. The content will be written
*dynamically* to the layers from the top frame where the element
specific content is compiled. When a user clicks an icon with a CSM
link they actually load a document (alt\_clickmenu.php with GET
parameters) into the top frame which will create the HTML for the menu
layer and then write it back through JavaScript to the <div> layers in
the calling document.

This solution means that CSMs don't have any significant performance
footprint on the script that implements a CSM. All that is needed is
some JavaScript in the <head> of the HTML document and the two <div>
layers for the dynamic menu HTML.

The fact that the top frame is used for generating the CSM can be seen
in browsers that does not support writing content dynamically to the
<div> layers in the calling document. For those browsers the top frame
will show the menu items in a horizontal order:

|img-146|

You can also enable this to happen even if the CSM HTML is also
written to the <div> layers. Just set this "User TSconfig"::

   options.contextMenu.options.alwaysShowClickMenuInTopFrame = 1


Adding elements to a Context Sensitive Menu
"""""""""""""""""""""""""""""""""""""""""""

For details on the `API for adding elements, please see "TYPO3 Core
API" <#Adding%20Context%20Sensitive%20Menu%20items%7Coutline>`_ .

