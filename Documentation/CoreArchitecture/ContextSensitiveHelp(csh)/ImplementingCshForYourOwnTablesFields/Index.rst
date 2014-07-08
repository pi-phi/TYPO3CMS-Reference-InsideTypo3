.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Implementing CSH for your own tables/fields
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Implementing CSH for tables and fields of a table is very easy. The
display of description, help icon etc. is automatically done by the
form rendering class as long as you do the configuration properly.
Lets look at two examples:


Adding CSH for fields added to existing tables
""""""""""""""""""""""""""""""""""""""""""""""

Say you have created an extension named "myext" and you have extended
the pages-table with a new field, "tx\_myext\_test". What you need to
do is to:

- Create a file named something like "locallang\_csh\_pages.xml" in your
  extension directory. Then enter XML code along these lines::

   <?xml version="1.0" encoding="UTF-8"?>
   <T3locallangExt>
     <data type="array">
       <languageKey index="en" type="array">
         <label index="tx_myext_test.description">Enter some test content</label>
         <label index="tx_myext_test.details">You can enter any content you like in this field</label>
       </languageKey>
     </data>
   </T3locallangExt>

- Then add this line to the ext\_tables.php file of your extension::

     t3lib_extMgm::addLLrefForTCAdescr('pages','EXT:myext/locallang_csh_pages.xml');

That's it.

