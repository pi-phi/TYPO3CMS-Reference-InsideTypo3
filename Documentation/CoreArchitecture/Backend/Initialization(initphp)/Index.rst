.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Initialization (init.php)
^^^^^^^^^^^^^^^^^^^^^^^^^


Scripts in TYPO3\_mainDir
"""""""""""""""""""""""""

Each script in the backend is  *required* to include the init.php
file. For core scripts this is done as the first code line in the
script::

   require ('init.php');

An example could be the alt\_main.php script (the backend frameset)::

   /**
   * Main frameset of the TYPO3 backend
   *
   * @author    Kasper Skårhøj <kasper@typo3.com>
   * Revised for TYPO3 3.6 2/2003 by Kasper Skårhøj
   */

   require ('init.php');
   require ('template.php');
   require_once (PATH_t3lib.'class.t3lib_loadmodules.php');
   require_once (PATH_t3lib.'class.t3lib_basicfilefunc.php');
   require_once ('class.alt_menu_functions.inc');



   // ***************************
   // Script Class
   // ***************************
   class SC_alt_main {
       var $content;
       var $mainJScode;
       var $loadModules;
       var $alt_menuObj;

These are comments on the various parts of the above source code:

- **init.php:** Included to provide database access, configuration
  values, class inclusions and user authentication etc.

- **template.php:** As you can see also the template.php script is
  included (which provides a class for backend HTML-output and
  processing of system languages/labels). The template.php script is
  typically included by all scripts which has some HTML-output for the
  backend interface.

- **Other classes:** Then further classes needed by the script depending
  on the function will be included.

- **Script Class:** Then a "script-class" (prefixed SC\_) is defined.
  This performs ALL processing done in the script. In the end of the
  script this class is instantiated and the output is written to the
  browser. That's it.


Scripts outside of TYPO3\_mainDir
"""""""""""""""""""""""""""""""""

For modules (located elsewhere than in the TYPO3\_mainDir) the
following initialization must be done  *prior to inclusion* of
init.php:

- **Global variable $BACK\_PATH** must  *point back* to the
  TYPO3\_mainDir (relative from the current script), eg. "../../" or
  "../../../typo3/"

- **Constant TYPO3\_MOD\_PATH** must  *point forth* to the location of
  the script (relative  *from* the TYPO3\_mainDir), eg.
  "ext/myextension/" or "../typo3conf/ext/myextension/"

An example is seen in the install/index.php file::

   define('TYPO3_MOD_PATH', 'install/');
   $BACK_PATH='../';

   require ($BACK_PATH.'init.php');

If a script is positioned outside of the TYPO3\_mainDir it must be in
the typo3conf/ directory. In that case the initial lines could look
like this::

   define('TYPO3_MOD_PATH', '../typo3conf/my_backend_script/');
   $BACK_PATH='../../typo3/';

   require ($BACK_PATH.'init.php');

**Modules**

Modules will typically initiate with basic lines like these::

   unset($MCONF);
   require ('conf.php');
   require ($BACK_PATH.'init.php');

So before init.php is called the local "conf.php" file is included.
That file must define the TYPO3\_MOD\_PATH constant and $BACK\_PATH
global variable. The modules section will describe this in detail.

We could take mod/web/perms/index.php as an example. Here the conf.php
file looks like this::

   <?php
   define('TYPO3_MOD_PATH', 'mod/web/perm/');
   $BACK_PATH='../../../';

   //... (additional configuration of module)...
   ?>

**Modules in typo3conf/**

Another example is from a conf.php file of a locally installed
extension (such are located in the "typo3conf/ext/" directory) with a
backend module::

   <?php

       // DO NOT REMOVE OR CHANGE THESE 3 LINES:
   define('TYPO3_MOD_PATH', '../typo3conf/ext/charsettool/mod1/');
   $BACK_PATH='../../../../typo3/';

   //... (additional configuration of module)...
   ?>


init.php
""""""""

So what happens in init.php?

**The short version is this:**

- A set of constants and global variables are defined.

- A set of classes are included.

- PHP environment is checked and set.

- Local configuration is included ("localconf.php").

- Table definitions are set ("tables.php").

- Connection to database established.

- Backend user is authenticated.

- Missing backend user authentication and other errors will make the
  script exit with an error message.

**The verbose version is this:**

(All global variables and constants referred to here are described in
" `TYPO3 Core API <#Variables%20and%20Constants%7Coutline>`_ ")

- Error reporting is set to ::

     error_reporting (E_ALL ^ E_NOTICE);

- Constants TYPO3\_OS, TYPO3\_MODE, PATH\_thisScript and TYPO3\_mainDir
  are defined.

- If TYPO3\_MOD\_PATH is defined the path is evaluated: The script must
  be found below either TYPO3\_mainDir or PATH\_site."typo3conf/".
  Otherwise the init.php script halts with an error message. Further the
  script will exit at this point if it was not able to get a correct
  absolute path for the installation. TYPO3  *requires* to know the
  absolute position of the directory from where the script is executed!

- Constants PATH\_typo3, PATH\_typo3\_mod, PATH\_site, PATH\_t3lib,
  PATH\_typo3conf are defined.

- Classes t3lib\_div and t3lib\_extMgm are included.

- t3lib/config\_default.php is included (shared with frontend as well).
  If no TYPO3\_db constant is defined after the inclusion of
  config\_default.php then the script exits with an error message.This
  is what happens inside config\_default.php:

  - t3lib/config\_default.php:

    ((""""""""""""""""""""""""""))

  - $TYPO3\_CONF\_VARS is initialized with the default set of values.

  - $typo\_db\* database variables are reset to blank.

  - PATH\_typo3conf.'localconf.php' is included. If not found, script
    exits with error message.

    - localconf.php:

      ((""""""""""""""))

    - localconf.php is allowed to override any variable from
      $TYPO3\_CONF\_VARS and further set the database variables with
      database username, password, database name, host.

    [Back in t3lib\_config\_default.php]:

  - Constants TYPO3\_db, TYPO3\_db\_username, TYPO3\_db\_password,
    TYPO3\_db\_host, TYPO3\_tables\_script, TYPO3\_extTableDef\_script and
    TYPO3\_languages is defined

  - $typo\_db\* variables are unset.

  - Certain $GLOBALS['TYPO3\_CONF\_VARS']['GFX'] values are manipulated.

  - debug() function is defined (only function outside a class!)

  - "ext\_localconf.php" files from installed extensions are included
    either as a cached file (ex.
    "typo3conf/temp\_CACHED\_ps5cb2\_ext\_localconf.php") or as individual
    files (depends on configuration of
    TYPO3\_CONF\_VARS['EXT']['extCache']."ext\_localconf.php" files are
    allowed to override $TYPO3\_CONF\_VARS values! They cannot modify the
    database connection information though. (See the definition of the
    Extension API for details)$TYPO3\_LOADED\_EXT is set.

  - Unsetting most of the reserved global variables ($PAGES\_TYPES,
    $ICON\_TYPES, $LANG\_GENERAL\_LABELS, $TCA, $TBE\_MODULES,
    $TBE\_STYLES, $FILEICONS, $WEBMOUNTS, $FILEMOUNTS, $BE\_USER,
    $TBE\_MODULES\_EXT, $TCA\_DESCR, $TCA\_DESCR, $LOCAL\_LANG) except
    $TYPO3\_CONF\_VARS (so from localconf.php files you cannot set values
    in these variables - you must use "tables.php" files).

  - Global vars $EXEC\_TIME, $SIM\_EXEC\_TIME and $TYPO\_VERSION are set

  [Back in init.php]:

- Database Abstraction Layer foundation class is included and global
  object, $TYPO3\_DB, is created.

- Global vars $CLIENT and $PARSETIME\_START are set.

- Classes for user authentication are included plus class for icon
  manipulation and the t3lib\_BEfunc (backend functions) class. Also the
  class "t3lib\_cs" for character set conversion is included.

- IP masking is performed (based on
  $TYPO3\_CONF\_VARS['BE']['IPmaskList']). Exits if criterias are not
  met.

- SSL locking is checked ($TYPO3\_CONF\_VARS['BE']['lockSSL']). Exits if
  criterias are not met.

- Checking PHP environment. Exits if PHP version is not supported or if
  HTTP\_GET\_VARS[GLOBALS] is set.

- Checking for Install Tool call: If constant TYPO3\_enterInstallScript
  is set, then the Install Tool is launched! Notice that the Install
  Tool is launched before any  *connection* is made to the database!
  Thus the Install Tool will run even if the database configuration is
  not complete or existing.

- Database connection. Exits if database connection fails.

- Checking browser. Must be 4+ browser. Exits if criterias are not met.

- Default tables are defined; PATH\_t3lib.'stddb/tables.php' is
  included! (Alternatively the constant TYPO3\_tables\_script could have
  defined another filename relative to "PATH\_typo3conf" which will be
  included instead. Deprecated since it spoils backwards compatibility
  and extensions should be used to override the default $TCA instead. So
  consider this obsolete.)

  - t3lib/stddb/tables.php:

    (("""""""""""""""""""""""))

  - global variables $PAGES\_TYPES, $ICON\_TYPES, $LANG\_GENERAL\_LABELS,
    $TCA, $TBE\_MODULES, $TBE\_STYLES, $FILEICONS are defined.

  [Back in init.php]

- "ext\_tables.php" files are included either as a cached file (ex.
  "typo3conf/temp\_CACHED\_ps5cb2\_ext\_tables.php") or as individual
  files (depends on configuration of
  TYPO3\_CONF\_VARS['EXT']['extCache'])."ext\_tables.php" files are
  allowed to override the global variables defined in
  "stddb/tables.php"! (See the definition of the Extension API for
  details)

- If the constant TYPO3\_extTableDef\_script is defined then that script
  is included.

- Backend user authenticated: Global variable $BE\_USER is instantiated
  and initialized. If no backend user is authenticated the script will
  exit (UNLESS the constant TYPO3\_PROCEED\_IF\_NO\_USER has been
  defined and set true prior to inclusion of init.php!)

- The global variables $WEBMOUNTS and $FILEMOUNTS are set (based on the
  BE\_USERS permissions)

- Optional output compression initialized

So that is what happens in init.php!

