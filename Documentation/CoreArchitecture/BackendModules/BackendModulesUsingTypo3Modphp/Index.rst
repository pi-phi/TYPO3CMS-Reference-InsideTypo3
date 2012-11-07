.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Backend modules using typo3/mod.php
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

With version 4.1 of TYPO3 there is a new and better framework for
integration of backend modules into the backend. The main principle
is, that all backend modules using this method are called through a
central script, “mod.php” in typo3/. This way, we get rid of the
trouble with conf.php files in need of modification when installing
extensions in local, global and system scopes.


Introduction
""""""""""""

Traditionally, a backend module runs directly from its own “index.php”
script (or named otherwise as set up with $MCONF['script']). In order
to initialize it must include the typo3/init.php file. Accessing this
file requires the module conf.php file to hold the “BACK\_PATH” to the
typo3/ directory. This will differ depending on where the extension
the module is in is installed: locally in typo3conf/ext/ or as a
global/system extension. So not only is the conf.php file changed by
the Extension Manager when installing extensions, it also makes it
very tricky and possibly error-prone to share local extensions between
sites with symlinks!

Using mod.php makes it all work differently. Examples in the core can
already be seen. For instance the “Tools > User Admin” uses this
method now. Instead of directly calling the script
“typo3/sysext/beuser/mod/index.php”, the script
“typo3/mod.php?M=tools\_beuser” is called which will look up (in
$TBE\_MODULES['\_PATHS']) which script is associated with
“tools\_beuser” and include that. The mod.php script also initializes
the backend, includes configuration and so on.


Adapting existing modules to this method
""""""""""""""""""""""""""""""""""""""""

Generally, you can create a module as you always did and then make
these changes:

- conf.php

  - Comment out (or remove!) the lines with the TYPO3\_MOD\_PATH and
    BACK\_PATH definitions. They are not needed anymore ($BACK\_PATH is
    blank for scripts running in typo3/ as mod.php
    does).Examples:#define('TYPO3\_MOD\_PATH',
    'sysext/beuser/mod/');#$BACK\_PATH='../../../';

  - Set the value of $MCONF['script'] to “\_DISPATCH”. This will make sure
    links to the module are pointed to “mod.php” instead of the real
    script of the module. This is only needed for modules appearing in the
    menu as a main- or submodule.Example:$MCONF['script']='\_DISPATCH';

- ext\_emconf.php

  - Remove the module name from the “module” entry in the array! This
    entry was what instructed the Extension Manager to modify
    TYPO3\_MOD\_PATH and BACK\_PATH in the conf.php file of the module
    during installation of the extension. Since this is not needed any
    more.

- Module script name

  - Must be “index.php” - but most modules will be that anyway. That's the
    convension.

- index.php (the module script)

  - In the module script you will have to comment out / remove those lines
    that are initializing the module:#unset($MCONF);#require
    ('conf.php');#require ($BACK\_PATH.'init.php');#require
    ($BACK\_PATH.'template.php');This is logical because this
    initialization is now done by mod.php.

  - Observe that the main script changed! When the module is calling it
    self, any hardcoded values for the script name (like
    “index.php?id=123”) must be changed. Now you must call
    “mod.php?M=[moduleKey]&id=123”. Its suggested you use
    htmlspecialchars($GLOBALS['MCONF']['\_']) as a reference to
    "thisScript" and add parameters like ."&par=val"

Context Menus: You will of course have to modify the clickmenu-class
to call "mod.php?M=[module name here]" where module name most
logically is the value of "$MCONF['name']" from the conf.php file.

Also, if you use this method for not-menu-modules, you must call
t3lib\_extMgm::addModulePath() from ext\_tables.php to register the
path of the module. Example:

t3lib\_extMgm::addModulePath('xMOD\_tximpexp',t3lib\_extMgm::extPath($
\_EXTKEY).'app/');

