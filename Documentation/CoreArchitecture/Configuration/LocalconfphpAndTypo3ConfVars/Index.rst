

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


localconf.php and $TYPO3\_CONF\_VARS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Configuration of TYPO3 is basically about setting values in the global
$TYPO3\_CONF\_VARS array. This is supposed to take place in the file
localconf.php located in the typo3conf/ directory (PATH\_typo3conf).
Furthermore, extensions can add content included in the same context
as the localconf.php by defining "ext\_localconf.php" files. See the
`Extension API for details
<#ext_tables.php%20and%20ext_localconf.php%7Coutline>`_ .

Typically a localconf.php file could look like this:

::

   <?php
   
       // Setting the Install Tool password to the default 'joh316'
   $TYPO3_CONF_VARS['BE']['installToolPassword'] = 'bacb98acf97e0b6112b1d1b650b84971';
       // Setting the list of extensions to BLANK (by default there is a long list set)
   $TYPO3_CONF_VARS['EXT']['extList'] = 'install';
   $TYPO3_CONF_VARS['EXT']['requiredExt'] = 'lang';
   
       // Setting up the database username, password and host
   $typo_db_username = 'root';
   $typo_db_password = 'nuwr875';
   $typo_db_host = 'localhost';
   
   ## INSTALL SCRIPT EDIT POINT TOKEN - all lines after this points may be changed by the install script!
   
   $typo_db = 't3_coreinstall';    //  Modified or inserted by Typo3 Install Tool.
   $TYPO3_CONF_VARS['SYS']['sitename'] = 'Core Install';    //  Modified or inserted by Typo3 Install Tool.
   // Updated by Typo3 Install Tool 14-02-2003 15:20:04
   $TYPO3_CONF_VARS['EXT']['extList'] = 'install,phpmyadmin,setup,info_pagetsconfig';       // Modified or inserted by Typo3 Extension Manager. 
   // Updated by Typo3 Extension Manager 19-02-2003 12:47:26
   ?>

In this example the lines until the "## INSTALL SCRIPT EDIT POINT
TOKEN..." were manually added during the setup of the installation.
But all lines after that point was added either by the Install Tool or
by the Extension Manager. You can also see how the Extension Manager
has overridden the formerly set value for "extList" - the list of
installed extensions. This line in localconf.php is automatically
found by the Extension Manager and next time an extensions is
installed/removed this line will be modified.

As you can see the localconf.php file must be writeable for the
Install Tool and Extension Manager to work correctly.

