.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


conf.php
^^^^^^^^

The "conf.php" file is used to configure both Backend Modules and
Stand-alone scripts - but not Function Menu modules (which are running
inside a backend modules environment!).

The file contains variable and constants definitions according to this
scheme:

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Variable/Constant
         Variable/Constant

   Description
         Description

   Examples
         Examples


.. container:: table-row

   Variable/Constant
         TYPO3\_MOD\_PATH

   Description
         PHP Constant.

         Defines the path  *from* the main backend folder (where init.php is,
         PATH\_typo3)  *to* the base folder of the module (where the conf.php
         file is).

         Used in init.php to determine the sitepath. Very, very important. If
         this is not correct, your module will not pass init.php without an
         error.

   Examples
         ::

              // Configures path for a core module:
            define('TYPO3_MOD_PATH',
                    'mod/web/info/');

              // Configures path for an extension module:
            define('TYPO3_MOD_PATH',
                    '../typo3conf/ext/temp/mod2/');


.. container:: table-row

   Variable/Constant
         $BACK\_PATH

   Description
         Global Variable.

         Defines the path "back" to the main folder (PATH\_typo3) from the
         module folder. Used by file references primarily. This is the reverse
         of "TYPO3\_MOD\_PATH".

   Examples
         ::

              // Configures backpath for a core module:
            $BACK_PATH = '../../../';

              // Configures backpath for extension module:
            $BACK_PATH = '../../../../typo3/';


.. container:: table-row

   Variable/Constant
         $MLANG

   Description
         Global variable containing title, descriptions and icon reference for
         the backend menu.

         *Applies only to Backend Modules.*

   Examples
         ::

            $MLANG['default']['tabs_images']['tab'] =
                    'moduleicon.gif';
            $MLANG['default']['ll_ref'] =
                    'LLL:EXT:temp/mod1/locallang_mod.php';


.. container:: table-row

   Variable/Constant
         $MCONF

   Description
         Global variable containing settings like access criteria, navigation
         frame script, default submodule and the module name.

         *Applies only to Backend Modules.*

   Examples
         ::

              // For the "Web" main module:
            $MCONF['defaultMod'] = 'list';
            $MCONF['navFrameScript'] = '../../alt_db_navframe.php';
            $MCONF['name'] = 'web';
            $MCONF['access'] = 'user,group';

              // More common for extension backend modules:
            $MCONF['access'] = 'user,group';
            $MCONF['script'] = 'index.php';


.. ###### END~OF~TABLE ######


Extensions and "conf.php" files
"""""""""""""""""""""""""""""""

When you create backend modules in extensions there is a tricky thing
to be aware of (exception: When using typo3/mod.php to dispatch to a
module, see later); The "conf.php" file has to change depending on
whether the extension is installed as "global"/"system" extension or
"local". The reason is that the TYPO3\_MOD\_PATH and $BACK\_PATH
values has to be different when an extension is in the "typo3conf/"
folder which is located outside the main TYPO3 directory, PATH\_typo3.
For instance TYPO3\_MOD\_PATH could look like
"../typo3conf/ext/myext/mod/" for a locally installed extensions while
it would be "ext/myext/mod/" for a globally installed extension!

If you install extensions via the Extension Manager this is no problem
since the Extension Manager (EM) corrects it before writing the
"conf.php" file to the servers file-system. But you need to make your
"conf.php" file compatible with this behaviour. Basically that
includes:

- Insert the two lines with "defined('TYPO3\_MOD\_PATH'......" and
  "$BACK\_PATH = ....." as the first ones and do not prefix or suffix
  them with anything; then the EM should be able to detect them.

- In the "ext\_emconf.php" file of the extension you need to add the
  directory of the module to the list of backend modules configured in
  the key $EM\_CONF[ *extension-key* ]['module'] - otherwise the EM will
  not know that there is a "conf.php" file to modify!

An example would look like this::

   <?php
       // DO NOT REMOVE OR CHANGE THESE 3 LINES:
   define('TYPO3_MOD_PATH', '../typo3conf/ext/temp/mod2/');
   $BACK_PATH='../../../../typo3/';
   $MCONF['name'] = 'web_txtempM2';

   $MCONF['access'] = 'user,group';
   $MCONF['script'] = 'index.php';
   $MLANG['default']['tabs_images']['tab'] = 'moduleicon.gif';
   $MLANG['default']['ll_ref"] = 'LLL:EXT:temp/mod2/locallang_mod.php';
   ?>


$MLANG
""""""

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   $MLANG keys
         $MLANG keys

   Description
         Description


.. container:: table-row

   $MLANG keys
         ::

            $MLANG['default']['tabs_images']['tab']

   Description
         Icon reference


.. container:: table-row

   $MLANG keys
         ::

            $MLANG['default']['ll_ref']

   Description
         "locallang" file reference where the keys "mlang\_tabs\_tab",
         "mlang\_labels\_tablabel" and "mlang\_labels\_tabdescr" defines titles
         and description text for the module.


.. container:: table-row

   $MLANG keys
         ::

            $MLANG[ language-key ]['labels']['tablabel']
            $MLANG[ language-key ]['labels']['tabdescr']
            $MLANG[ language-key ]['tabs']['tab']

   Description
         Obsolete


.. ###### END~OF~TABLE ######

The $MLANG variable contains the icon reference and title /
description for a Backend Module. Originally the $MLANG variable
defined values for all languages inside the conf.php file. This
(obsolete) codelisting shows it::

   $MLANG['default']['labels']['tablabel'] = 'Advanced functions';
   $MLANG['default']['tabs']['tab'] = 'Func';
   $MLANG['default']['tabs_images']['tab'] = 'func.gif';

   $MLANG['dk']['labels']['tablabel'] = 'Avancerede funktioner';
   $MLANG['dk']['tabs']['tab'] = 'Funk.';

   $MLANG['de']['labels']['tablabel'] = 'Erweiterte Funktionen';
   $MLANG['de']['tabs']['tab'] = 'Funk.';

   $MLANG['no']['labels']['tablabel'] = 'Avanserte funksjoner';
   $MLANG['no']['tabs']['tab'] = 'Funk.';

   $MLANG['it']['labels']['tablabel'] = 'Funzioni avanzate';
   $MLANG['it']['tabs']['tab'] = 'Funzione';
   ...

   (OBSOLETE!)

This is still supported for backwards compatibility reasons. Today you
need to configure only two lines, one for a "locallang" file reference
and one for the icon image::

   $MLANG['default']['tabs_images']['tab'] = 'func.gif';
   $MLANG['default']['ll_ref']='LLL:EXT:lang/locallang_mod_web_func.php';

The icon reference (line 1) points to an icon image relative to the
current directory (normally located there).

The "locallang" file reference in line 2 points to a "locallang"-file
which in this case looks like this::

   <?php
   # TYPO3 CVS ID: $Id: locallang_mod_web_func.php,v 1.5 2004/04/30 16:19:54 typo3 Exp $
   $LOCAL_LANG = Array (
       'default' => Array (
           'title' => 'Advanced functions',
           'clickAPage_content' => 'Please click a page title in the page tree.',
           'mlang_labels_tablabel' => 'Advanced functions',
           'mlang_labels_tabdescr' => 'You\'ll find general export and import functions here. ... sorting of pages.',
           'mlang_tabs_tab' => 'Functions',
       ),
       'dk' => Array (
           'title' => 'Avancerede funktioner',
           'clickAPage_content' => 'Klik på en sidetitel i sidetræet.',
           'mlang_labels_tablabel' => 'Avancerede funktioner',
           'mlang_labels_tabdescr' => 'Her vil du finde generelle eksport og import funktioner. ... sortering af sider.',
           'mlang_tabs_tab' => 'Funktioner',
       ),
   ...
   );
   ?>

In this locallang file, some keys are reserved words that point out
information related to the "conf.php" file:

- **mlang\_tabs\_tab** : Title of the module in the menu.

- **mlang\_labels\_tablabel** : Long title of the module. Used as
  "title" attribute for menu link and title in the "About modules" list.

- **mlang\_labels\_tabdescr** : Description of the module (used in
  "About modules")


$MCONF
""""""

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   $MCONF keys
         $MCONF keys

   Description
         Description


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['name']

   Description
         Module name.

         - For main modules this is [ *module-key* ]

         - For sub modules this is [ *module-key* ]\_[ *sub-module-key* ]

         - For Stand-Alone scripts, prefixed "xMOD\_" and then probably the file-
           name or another unique identification.

         **Examples (Backend Modules):** ::

              // Main module (from extension)
            $MCONF['name'] = 'txtempM1';

              // Submodule of "Web" main module:
            $MCONF['name'] = 'web_txtempM2';

              // File > Filelist module:
            $MCONF['name'] = 'file_list';

         **Example (Stand-alone scripts):** ::

              // Setting pseudo module name
            $this->MCONF['name'] = 'xMOD_alt_clickmenu.php';
              // Setting pseudo module name for CSM item
            $MCONF['name'] = 'xMOD_tx_temp_cm1';


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['script']

   Description
         Defines the PHP script which the module is run by. The backend will
         link to this script when the module is activated.

         Special keyword is "\_DISPATCH" which will indicate that the
         "typo3/mod.php" script is used to access the module.


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['access']

   Description
         Defines access criteria by list of keywords. If "admin", only admin-
         users have access. If "user", "group" or "user,group" then the module
         is by default inaccessible.

         - "admin" : For "admin" users only.

         - "user" : Configurable for backend users.

         - "group" : Configurable for backend groups.

         - [blank]: Everyone has access.

         **Example:**

         "user,group" - No one (except "admin") has access  *except* the module
         is specifically added in their user / group profile.

         This is how the Module selector looks for both backend users and
         groups:

         |img-86|

         (For Backend Usergroups you have to enable "Include Access Lists" in
         order to access the module selector).


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['workspaces']

   Description
         Defines which workspaces the module is allowed to work under. Empty
         string means all workspaces. Otherwise this list of keywords can be
         combined to set access:

         - "online" : Available in Live (online) mode

         - "offline" : Available in Draft (offline) mode

         - "custom" : Available for custom modes


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['defaultMod']

   Description
         Sub-module key of sub-module to be default for main module. (Only for
         Main modules)


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['navFrameScript']

   Description
         If set, the module will become a "Frameset" module and this will point
         to the script running in the navigation frame. (Only for Main modules)

         **Example (From "Web" main module):** ::

            $MCONF['navFrameScript'] = '../../alt_db_navframe.php';


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['navFrameScriptParam']

   Description
         GET parameters to pass to the navigation frame script (only Sub-
         modules of a frameset module).

         Parameters set for the main module will be inherited to submodules if
         not overridden.


.. container:: table-row

   $MCONF keys
         ::

            $MCONF['shy']

   Description
         If TRUE then the module will not be visible in the backend menu or
         anywhere modules are displayed based on the processing of
         t3lib\_loadModules::load()


.. ###### END~OF~TABLE ######


Example: conf.php for Stand-Alone backend scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The difference between a stand-alone backend script and a backend
module is that the backend module has an API for access control and a
menu item. But they share the same requirements for basic
initialization.

The most basic configuration for a backend script is setting the
TYPO3\_MOD\_PATH constant and the $BACK\_PATH variable before
including "init.php". The script "typo3/install/index.php" is an
example of this::

   define('TYPO3_MOD_PATH', 'install/');
   $BACK_PATH = '../';
   ...
   require('../init.php');

It is more common to define the TYPO3\_MOD\_PATH constant and
$BACK\_PATH variable in a separate conf-file - that is always done for
modules and when you are supplying backend scripts from extensions. In
such a case the initialization of the backend script will look like
this::

   unset($MCONF);
   require('conf.php');
   require($BACK_PATH . 'init.php');
   ...

The file "conf.php" looks like this::

   <?php
       // DO NOT REMOVE OR CHANGE THESE 3 LINES:
   define('TYPO3_MOD_PATH', '../typo3conf/ext/temp/cm1/');
   $BACK_PATH = '../../../../typo3/';
   $MCONF['name'] = 'xMOD_tx_temp_cm1';
   ?>

The line defining $MCONF['name'] is optional since the script is a
stand-alone script. It might be used as a key for Function menus or
otherwise. You can tell that it is a pseudo module name since it is
prefixed "xMOD\_".

The main point of TYPO3\_MOD\_PATH and $BACK\_PATH is to set the
environment so TYPO3 knows the position of the backend script in
relation to the main backend folder, PATH\_typo3. And the inclusion of
"init.php" is required in order to initialize the backend environment
and authenticate the backend user. If the script returns from
"init.php" it went well and you can be safe that a backend user is
logged in (unless configured otherwise).


Example: conf.php for Backend Modules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The conf.php file for a backend module compared to a stand-alone
script is different mainly by defining values for $MCONF and $MLANG.
This is an example::

   <?php
       // DO NOT REMOVE OR CHANGE THESE 3 LINES:
   define('TYPO3_MOD_PATH', '../typo3conf/ext/temp/mod2/');
   $BACK_PATH = '../../../../typo3/';
   $MCONF['name'] = 'web_txtempM2';

   $MCONF['access'] = 'user,group';
   $MCONF['script'] = 'index.php';
   $MLANG['default']['tabs_images']['tab'] = 'moduleicon.gif';
   $MLANG['default']['ll_ref'] = 'LLL:EXT:temp/mod2/locallang_mod.php';
   ?>

It doesn't do any difference whether the module is a main- or sub-
module. Only the $MCONF['name'] will change in that case.

