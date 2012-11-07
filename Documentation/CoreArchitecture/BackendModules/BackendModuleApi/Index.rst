.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Backend Module API
^^^^^^^^^^^^^^^^^^


$TBE\_MODULES
"""""""""""""

In TYPO3 all modules are configured in the global variable,
$TBE\_MODULES (see t3lib/stddb/tables.php). $TBE\_MODULES contains the
structure of the backend modules as they are arranged in main- and
sub-modules. Every entry in this array represents a menu item on
either first level (array key) or second level (value from list) in
the left menu in the TYPO3 backend. ::

   $TBE_MODULES = Array (
       'web' => 'list,info,perm,func',
       'file' => 'list',
       'doc' => '',    // This should always be empty!
       'user' => '',
       'tools' => 'em',
       'help' => 'about,cshmanual'
   );

The syntax is::

   $TBE_MODULES[ module ] => "submodule_1,submodule_2,submodule_3,submodule_4"

There are two special keys in the $TBE\_MODULES array to be aware of:

- **$TBE\_MODULES['\_PATHS']** is an array used by extensions to
  register module file locations (for backend modules located in
  extensions). Obviously, this is not representing a main module.

- **$TBE\_MODULES['doc']** is a main module which cannot have any sub
  modules.


Module file locations
"""""""""""""""""""""

Modules can be located in the file system after three different
principles:

- **Core modules** The file location of the core modules is
  "typo3/mod/". Here you will find a number of folders (main modules)
  and sub-folders (sub modules) with "conf.php" files and icons in. It's
  unlikely that new core modules are added since extensions should
  provide all future modules. You should never add core modules by
  yourself.Core modules are arranged in folders after the schemes
  "typo3/mod/ *[module]* " and "typo3/mod/ *[module]/[submodule]* ".

- **User defined modules (OBSOLETE)** Modules located in "../typo3conf/"
  directory after the same principles as core modules (typo3conf/
  *[module key]* / *[sub-module key]* ). If a module or sub-module key
  in $TBE\_MODULES is  *not* found in "typo3/mod/" then it is looked for
  in "../typo3conf/". Module/Sub-module keys of user defined modules
  should be prefixed with a lowercase "u", eg. "web\_uEtest" (located in
  "typo3conf/web/uEtest/" or "uMaintest" (located in
  "typo3conf/uMaintest")( *Deprecated concept; Do not create user
  defined modules any more! Create modules in extensions instead.)*

- **Modules from extensions** Custom modules supplied from extensions
  are located somewhere inside the extension file space. The extension
  adds the module to the system by an API call in the "ext\_tables.php"
  file. The API call will add the module key to the $TBE\_MODULES array
  and set an entry in $TBE\_MODULES['\_PATH'] pointing to the absolute
  path for the module.


Parsing $TBE\_MODULES
"""""""""""""""""""""

The backend determines if a module is a core/user or extension module
by first looking for a path-entry in $TBE\_MODULES['\_PATHS'] using "
*[module]\_[submodule]"* as key (this is also the "name" of the
module). If an entry is found, this location is set as the path.
Otherwise "t3lib\_loadmodules" will look first for the module in the
core location ("typo3/mod/") and if not found, then in
"../typo3conf/".

In any case, a module is only detected if a **"conf.php" file** was
found in its filepath! This file contains configuration of the module;
The module name, script, access criteria, type etc.

When the backend needs to get a list of available modules for a
backend user the class "t3lib\_loadmodules" is used. This code snippet
does the trick::

       // Backend Modules:
   $loadModules = t3lib_div::makeInstance('t3lib_loadModules');
   $loadModules->load($TBE_MODULES);
   foreach($loadModules->modules as $mainMod => $info)    {
      ...
   }

The array $loadModules->modules contains information about the modules
that were accessible; their names, types, sub modules (if any) and the
filepath to their scripts (relative to PATH\_typo3).


Registering new modules
"""""""""""""""""""""""

Adding new modules should be done by extensions. The API is easy; in
the "ext\_tables.php" file of the extension you simply need to add
code like this:

**For main modules:** ::

   if (TYPO3_MODE=='BE')    {
       t3lib_extMgm::addModule('txtempM1','','',t3lib_extMgm::extPath($_EXTKEY).'mod1/');
   }

"txtempM1" is the module key of the main module created. It could
appear like this in the menu:

|img-83|

**For sub modules:** ::

   if (TYPO3_MODE=='BE')    {
       t3lib_extMgm::addModule('web','txtempM2','',t3lib_extMgm::extPath($_EXTKEY).'mod2/');
   }

"web" is the name of the main module (the "Web>" module) and
"txtempM2" is the sub-module key. In the menu this module could appear
like this:

|img-84|

After such two modules has been added the $TBE\_MODULES array could
look like this:

|img-85|

Notice that "txtempM1" became a key in the array (main modules) and
"txtempM2" was added to the list of modules in the "Web" main module
(sub-modules are listed). Also notice that the "\_PATHS" key contains
an array of file locations of all the modules that are coming from
extensions! The last two entries in the list defines the locations of
the two modules from our example!

