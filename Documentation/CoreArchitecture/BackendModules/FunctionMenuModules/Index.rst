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


Function Menu modules
^^^^^^^^^^^^^^^^^^^^^

Function Menu modules are integrated in existing backend modules that
supports this feature. In the core the modules Web>Info and
Web>Function does so. Also Web>Template and even User>Taskcenter does!

Function Menu modules are accessed through the function menu of the
host module:

|img-81|

In this example the Web>Functions module is the host backend module
and the selector box in the upper right corner shows the two Function
menu modules attached to Web>Functions. It turns out that the function
menu module "Wizards" supports even another level of externally
attached scripts - a "second level Function Menu module". The API for
adding elements to the second level is the same as for the first.


Attaching Function Menu modules to the host backend module
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Function Menu modules live in the environment of the host backend
module. Therefore they have no conf.php files etc. All they do is to
supply a PHP class which is called when they need to be activated.
Like any other module they have to render the content and return it
then.

Attaching Function Menu modules to a host backend module is done by
adding some values to an array in the global scope. To make this easy
there is API function calls to do that which you should use. To create
a Function Menu on the first level you would include this code in the
"ext\_tables.php" file of the extension:

::

   if (TYPO3_MODE=='BE')    {
       t3lib_extMgm::insertModuleFunction(
           'web_func',        
           'tx_temp_modfunc1',
           t3lib_extMgm::extPath($_EXTKEY).'modfunc1/class.tx_temp_modfunc1.php',
           'LLL:EXT:temp/locallang_db.php:moduleFunction.tx_temp_modfunc1'
       );
   }

If you want to insert it on the second level this would be used (for
the Wizards example above):

::

   if (TYPO3_MODE=='BE')    {
       t3lib_extMgm::insertModuleFunction(
           'web_func',        
           'tx_temp_modfunc2',
           t3lib_extMgm::extPath($_EXTKEY).'modfunc2/class.tx_temp_modfunc2.php',
           'LLL:EXT:temp/locallang_db.php:moduleFunction.tx_temp_modfunc2',
           'wiz'    
       );
   }

Notice the only difference; The addition of the fifth argument in the
function call pointing to the first level Function Menu item.


Basic framework
"""""""""""""""

The Function Menu module code is found in a class in the scripts
pointed to in the configuration. Such a class extends the class
"t3lib\_extobjbase" which is designed to handle all the basic
management of a Function Menu module.

A basic framework for a Function Menu module looks like this:

::

      1: require_once(PATH_t3lib."class.t3lib_extobjbase.php");
      2: 
      3: class tx_temp_modfunc1 extends t3lib_extobjbase {
      4:     function modMenu()    {
      5:         global $LANG;
      6:         
      7:         return Array (
      8:             "tx_temp_modfunc1_check" => "",
      9:         );        
     10:     }
     11: 
     12:     function main()    {
     13:             // Initializes the module. Done in this function because we may need to re-initialize if data is submitted!
     14:         global $SOBE,$BE_USER,$LANG,$BACK_PATH,$TCA_DESCR,$TCA,$CLIENT,$TYPO3_CONF_VARS;
     15:         
     16:         $theOutput.=$this->pObj->doc->spacer(5);
     17:         $theOutput.=$this->pObj->doc->section($LANG->getLL("title"),"Dummy content here...",0,1);
     18:         
     19:         $menu=array();
     20:         $menu[]=t3lib_BEfunc::getFuncCheck($this->pObj->id,"SET[tx_temp_modfunc1_check]",$this->pObj->MOD_SETTINGS["tx_temp_modfunc1_check"]).$LANG->getLL("checklabel");
     21:         $theOutput.=$this->pObj->doc->spacer(5);
     22:         $theOutput.=$this->pObj->doc->section("Menu",implode(" - ",$menu),0,1);
     23: 
     24:         return $theOutput;
     25:     }
     26: }
     27: 
     28: 
     29: 
     30: if (defined("TYPO3_MODE") && $TYPO3_CONF_VARS[TYPO3_MODE]["XCLASS"]["ext/temp/modfunc1/class.tx_temp_modfunc1.php"])    {
     31:     include_once($TYPO3_CONF_VARS[TYPO3_MODE]["XCLASS"]["ext/temp/modfunc1/class.tx_temp_modfunc1.php"]);
     32: }

From the code you might be able to figure out that the host backend
module is available as the object reference $this->pObj. In this code
listing it is used to access the document template object for
rendering the output.


More details
""""""""""""

More details about Function Menu modules and the framework of
"t3lib\_extobjbase" is found in extension programming tutorials and
inside the class "t3lib\_extobjbase" itself!

