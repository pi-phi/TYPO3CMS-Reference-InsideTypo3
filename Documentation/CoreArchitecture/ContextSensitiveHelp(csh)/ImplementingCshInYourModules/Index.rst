.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Implementing CSH in your modules
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Implementing CSH in your own modules is a little more difficult. In
addition to the two mandatory steps of a) creating a
locallang\_csh\_\*.php file in your extension directory and b) calling
the t3lib\_extMgm::addLLrefForTCAdescr() API function in the
ext\_tables.php file you might also have to manually  *load* the
labels and manually  *insert* the labels where you want them to
appear. Whether you need this step or not depends on your method of
application:


Method 1: Using t3lib\_BEfunc::helpText\*() functions
"""""""""""""""""""""""""""""""""""""""""""""""""""""

If you use these functions the descriptions are not loaded
automatically for you. You have to do that manually in the
initialization of your module:

#. First, load the description labels for the module. You do that best in
   the init() function of your script class::

                         // Descriptions:
                      $this->descrTable = "_MOD_".$this->MCONF["name"];
                      if ($BE_USER->uc["edit_showFieldHelp"])      {
                              $LANG->loadSingleTableDescription($this->descrTable);
                      }

   It's assumed that $this->MCONF equals the global $MCONF var that
   contain module configuration - this delivers the unique module name.

   Then secondly -  *but most important* - is that you check for the User
   Configuration setting "edit\_showFieldHelp" (highlighted with red)

#. Then for each position in your document where you want to have a help
   icon and possibly help-text (description field) you will have to call
   an API function; t3lib\_BEfunc::helpTextIcon(),
   t3lib\_BEfunc::helpText() or both. These will check if help is
   available and if so, return a help icon / help text.

This approach is user in the Extension Manager for example. Here it is
a good choice because there are descriptions for all settings for
extensions and we want to link them to the help icons in a table
column


Example 1
~~~~~~~~~

The most simple and straight forward way to include the icon/helptext
would be something like this::

   $HTMLcode.=
           t3lib_BEfunc::helpTextIcon($this->descrTable,"quickEdit_selElement",$GLOBALS["BACK_PATH"]).
           t3lib_BEfunc::helpText($this->descrTable,"quickEdit_selElement",$GLOBALS["BACK_PATH"]).
           "<br/>";

These lines assumes that

- $this->descrTable points to the "tablename" (in this case the string
  "\_MOD\_".$MCONF["name"])

- "quickEdit\_selElement" is a "fieldname" defined in the locallang\_csh
  file

- $GLOBALS["BACK\_PATH"] is correctly pointing back to the
  TYPO3\_mainDir (that is necessary for modules outside of the main
  directory)

The locallang\_csh file for this example would look like this::

   <?php
   /**
   * Default  TCA_DESCR for "_MOD_web_layout"
   */

   $LOCAL_LANG = Array (
       'default' => Array (
           'quickEdit.description' => 'The Quick Editor gives you direct . . . ',
           'quickEdit.details' => 'The Quick Editor is designed to cut . . .',
           'quickEdit_selElement.description' => 'This is an overview of th. . . ',
           'columns.description' => 'By the \"Columns\" view you can control t. . . ',
       ),
   );
   ?>

(Location is "sysext/cms/locallang\_csh\_weblayout.php" and in
ext\_tables.php for the "cms" extension you will find this line to
associate the locallang file with CSH for the Web>Page module: t3lib\_
extMgm::addLLrefForTCAdescr('\_MOD\_web\_layout','EXT:cms/locallang\_c
sh\_weblayout.php'); )

Notice the key " quickEdit\_selElement.description" which will provide
the description for the help icon in the example.


Example 2
~~~~~~~~~

A more advanced - and better - approach is to create a function
internally in the script class of the module for handling the help
texts. This is an example from the Extension Manager module
(mod/tools/em/index.php)::

   function helpCol($key)    {
       global $BE_USER;
       if ($BE_USER->uc["edit_showFieldHelp"])    {
           $hT = trim(t3lib_BEfunc::helpText($this->descrTable,"emconf_".$key,$this->doc->backPath));
           return '<td>'.
               ($hT?$hT:
                   t3lib_BEfunc::helpTextIcon(
                       $this->descrTable,
                       "emconf_".$key,
                       $this->doc->backPath
                   )).
               '</td>';
       }
   }

The basic elements are the same, but its more comfortable to work
with.

If you want more examples you can make a source code search for the
function ->loadSingleTableDescription and $TCA\_DESCR and then you
should find a number of examples to learn from as well.


Method 2: Using t3lib\_BEfunc::cshItem()
""""""""""""""""""""""""""""""""""""""""

This is the quick method. Calling this function instead of
t3lib\_BEfunc::helpText() will deliver an output which is either a
help-icon or a table with both icon and description text depending on
the current users configuration. In addition it will automatically
load the description files for the $table parameter given. ::

   $HTMLcode.=
   t3lib_BEfunc::cshItem($tableIdent,'quickEdit',$BACK_PATH);

