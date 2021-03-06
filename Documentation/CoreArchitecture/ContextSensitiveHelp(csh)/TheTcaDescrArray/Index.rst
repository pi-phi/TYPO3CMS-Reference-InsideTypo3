.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


The $TCA\_DESCR array
^^^^^^^^^^^^^^^^^^^^^

The global array $TCA\_DESCR is reserved to contain CSH labels. CSH
labels are loaded as they are needed. Thus the class rendering the
form will make an API call to the $GLOBALS['LANG'] object to have the
CSH labels loaded - if any - for the table "pages".

In this process the $TCA\_DESCR array will look like this before the
API call:

|img-135|

Notice that the key ['pages']['refs'] has a file reference pointing to
a locallang file which contains the labels we need. Nothing more.
These default values found in $TCA\_DESCR is set by API calls in
t3lib/stddb/tables.php::

   /**
    * Setting up TCA_DESCR - Context Sensitive Help
    */
   t3lib_extMgm::addLLrefForTCAdescr('pages', 'EXT:lang/locallang_csh_pages.xml');
   t3lib_extMgm::addLLrefForTCAdescr('be_users', 'EXT:lang/locallang_csh_be_users.xml');
   t3lib_extMgm::addLLrefForTCAdescr('be_groups', 'EXT:lang/locallang_csh_be_groups.xml');
   t3lib_extMgm::addLLrefForTCAdescr('sys_filemounts', 'EXT:lang/locallang_csh_sysfilem.xml');
   t3lib_extMgm::addLLrefForTCAdescr('_MOD_tools_em', 'EXT:lang/locallang_csh_em.xml');

The red line above is the line setting the file for the "pages" table.
Notice that other extensions might supply additional files and add
additional files to be includes after the defaults ones above! In that
case those will override/add to the existing values. The extension
"context\_help" is doing just that - it includes a whole bunch of
locallang files with description of basically the whole "cms"
extension.

Well, inside of the class t3lib\_TCEforms an API call is made to load
the actual labels for the pages table::

                      if ($this->edit_showFieldHelp || $this->doLoadTableDescr($table)) {
                                   $GLOBALS['LANG']->loadSingleTableDescription($table);
                           }

So labels for $table is loaded - and if table is "pages" then this
will be the result back in $TCA\_DESCR:

As you can see labels are loaded from the file
sysext/lang/locallang\_csh\_pages.xml. The content of this file looks
like this (partly)::

   <?xml version="1.0" encoding="UTF-8"?>
   <T3locallangExt>
     <data type="array">
       <languageKey index="en" type="array">
         <label index="title.description">Enter the title of the page or folder.</label>
         <label index="title.syntax">You must enter a page title. The field is required.</label>

         <label index="doktype.description">Select the page type. This affects . . . ses.</label>
         <label index="doktype.details">The 'Standard' type represents a . . . any problems).</label>

         <label index="TSconfig.description">Page TypoScript configuration.</label>
         <label index="TSconfig.details">Basically 'TypoScript' is a . . . alled</label>

         <label index="TSconfig.syntax">Basic TypoScr. . . 'Conditions' and 'Constants'.</label>
       </languageKey>
     </data>
   </T3locallangExt>

Notice how the actual labels in the locallang file contains periods
(.) which defines [fieldname].[type-key].[special options]

- **Fieldname** is the field from the table in question

- **Type-key** is one of these values:

  - **description** : A short description of the field (as shown in the
    editing form)

  - **details** : A more lengthy description adding some details. Only
    visible in the external popup window.

  - **syntax** : A description of the syntax of the content in the field
    in question. Use this if the field must have some special code format
    entered.

  - **image** : A reference to an image

  - **image\_descr** : Description for the image

  - **seeAlso** : References to other relevant CSH entries.

  - **alttitle** : Alternative title for field/table

- **special options** : Here you can add for example a plus-sign '+'.
  Means the value of the label is not substituting any existing value
  but rather adding to it (separated with a single line break). This
  makes sense only if you are supplying overriding values for existing
  previously loaded values.

**Notice:**

A field key can be prefixed with "\_" which will prevent it from being
shown in the translation tools. This is useful for "seeAlso" and
"image" since they should not be translated to other languages!


HTML in CSH
"""""""""""

Currently "description", "details" and "syntax" fields accept limited
XHTML content: <strong>, <em>, <b>, <i>. However, don't use important
markup for the "description" field since it will stripped when shown
in TCEforms.


Example
~~~~~~~

Looking at the "context\_help" extension you will see many
"locallang\_csh\_\*.xml" files. One is named
"locallang\_csh\_pages.xml" and the first lines from that looks like
this::

   <?xml version="1.0" encoding="UTF-8"?>
   <T3locallangExt>
     <data type="array">
       <languageKey index="en" type="array">
         <label index="title.description.+">This is normally shown in the website navigation.</label>
         <label index="layout.description">Select a layout for the page. Any effect depends on the website template.</label>

Notice the red plus-sign in the "title.description" label - this value
is  *added* to the existing title.

The other key, "layout.description", is an addition which did not
previously exist in the $TCA\_DESCR for the pages-table - but that
makes sense here since the "context\_help" depends on the "cms"
extension being loaded which would have added the field "layout" to
the database on beforehand! (the "layout" field in the pages-table is
not a part of the core as you might have guessed by now...)


Keys in $TCA\_DESCR
"""""""""""""""""""

The keys in $TCA\_DESCR is by default pointing to database tables, for
example "pages". However if you wish to use CSH in your modules you
can use keys name by this syntax::

      _MOD_[module_name] - Placed in the "Backend module" category
           xMOD_[extension key with tx_ infront] - Placed in the "Other" category
           xEXT_[extension key] - for description of extensions.
           xGLOSSARY_[group] - for glossaries, will be marked up in other CSH.

Normally modules will have their name in the $MCONF variable. That
would allow you to load the available labels for your module by this
API call::

   $key = '_MOD_' . $MCONF['name'];
   $GLOBALS['LANG']->loadSingleTableDescription($key);

... and you would now have your labels loaded in
$TCA\_DESCR[$key]['columns'].

**Notice:** You will still have to set up the locallang file with the
CSH labels by a API call to t3lib\_extMgm::addLLrefForTCAdescr(),
possibly in a "ext\_tables.php" file.

