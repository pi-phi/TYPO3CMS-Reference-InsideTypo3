

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


The Module script
^^^^^^^^^^^^^^^^^


Main framework of a Backend Module or Stand-Alone script
""""""""""""""""""""""""""""""""""""""""""""""""""""""""

After the initialization a Backend Module or Stand-Alone script can
contain any custom PHP code you wish. However most scripts from the
core and system extensions will follow the same model as all other
backend modules. An example looks like this:

::

     29:     // DEFAULT initialization of a module [BEGIN]
     30: unset($MCONF);
     31: require('conf.php');
     32: require($BACK_PATH.'init.php');
     33: require($BACK_PATH.'template.php');
     34: $LANG->includeLLFile('EXT:temp/cm1/locallang.php');
     36: require_once (PATH_t3lib.'class.t3lib_scbase.php');
     37:     // ....(But no access check here...)
     38:     // DEFAULT initialization of a module [END]
   ...
     40: class tx_temp_cm1 extends t3lib_SCbase {
   ...
    132: }
    133: 
    134: 
    135: 
    136: if (defined('TYPO3_MODE') && $TYPO3_CONF_VARS[TYPO3_MODE]['XCLASS']['ext/temp/cm1/index.php'])    {
    137:     include_once($TYPO3_CONF_VARS[TYPO3_MODE]['XCLASS']['ext/temp/cm1/index.php']);
    138: }
    139: 
    140: 
    141: 
    142: 
    143: // Make instance:
    144: $SOBE = t3lib_div::makeInstance('tx_temp_cm1');
    145: $SOBE->init();
    146: 
    147: 
    148: $SOBE->main();
    149: $SOBE->printContent();

- Lines 30-32 does the basic initialization

- Line 33 includes the backend document template class and language
  class (provides the $LANG and $TBE\_TEMPLATE objects).

- Line 34 includes the main "locallang" file for the script

- Line 36 includes the base class for the class in the script

- Line 37 is where you should do your access check if you want to apply
  any.

- Line 40 to 132 defines the class that is called to create all output
  from this file. Notice that it extends "t3lib\_SCbase" which is normal
  (but not required!) for backend modules and stand-alone scripts. The
  "SCbase" class provides some APIs for various things you often need.

- Line 136-138 checks for XCLASS extensions of the scripts class.

- Finally, line 144-149 instantiates the script class and calls the
  methods inside to render and output the content.


Checking for module access
""""""""""""""""""""""""""

If the script is a true backend module you should check for module
access in line 37 where there is currently just a comment. The access
is easily checked by this API function where you simply give the
$MCONF array as argument. The function will check what kind of access
criteria are in the $MCONF array and then evaluate the situation
accordingly. In this case it will exit with a an error message if the
user is not logged in.

::

     // This checks permissions and exits if the users has no permission for entry.
   $BE_USER->modAccess($MCONF,1);


Checking for "admin" user
"""""""""""""""""""""""""

In case your backend script requires the "admin" user to be logged in
it is easy to do a check:

::

   if (!$BE_USER->isAdmin()) die('No access for you...');

See the `API for the $BE\_USER object
<#Backend%20User%20Object%7Coutline>`_ for more details.


More details
""""""""""""

Please refer to the comments inside of the class file
"t3lib/class.t3lib\_scbase.php" for more details on a basic framework
for backend modules ("script classes"). If you want to start a new
backend module you should definitely use the Kicstarter Wizard to do
so. It will set up all the basics for you.

