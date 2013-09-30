.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


.. _initialize-cli-mode:

Initialize TYPO3 backend in a PHP shell script (CLI mode)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most scripts in TYPO3 expect to be executed from a web browser.
However you might need to create a PHP script which is executed in a
Unix shell as a cronjob. In itself PHP is capable of that as long as
PHP was also compiled as a binary (typically "/usr/bin/php") but you
need to do some tricks in order to initialize TYPO3s backend
environment.


Tricky script path
""""""""""""""""""

The greatest challenge is to make the script recognize its own path.
This is necessary for all includes afterwards. It seems that the path
of the script is available as the variable $\_ENV['\_'] in most cases.
However it changes value depending on how you call the script. In
order to make life easy for our programming we decide that the script
must always be executed by its absolute path. So
"./myphpshellscript.phpsh" will not work, but
"/abs/path/to/typo3conf/ext/myext/ myphpshellscript.phpsh" will.

**Note about FreeBSD:** It has been reported (by Rainer Kuhn, punkt.de
– thanks) that on FreeBSD the path is not available in $\_ENV['\_']
but can be extracted from $\_SERVER['argv'][0]. Generally there are
not enough experience and knowledge about this issue to state
something final, but for now we suggest a fall back solution as seen
below where $\_ENV['\_'] is tested and if not found, falls back to
$\_SERVER['argv'][0]


Basic framework
"""""""""""""""

To set up a PHP shell script that initializes the TYPO3 you create a
file with the framework here::

      1: #! /usr/bin/php -q
      2: <?php
      3:
      4: // *****************************************
      5: // Standard initialization of a CLI module:
      6: // *****************************************
      7:
      8:     // Defining circumstances for CLI mode:
      9: define('TYPO3_cliMode', TRUE);
     10:
     11:     // Defining PATH_thisScript here: Must be the ABSOLUTE path of this script in the right context:
     12:     // This will work as long as the script is called by it's absolute path!
     13: define("PATH_thisScript", $_ENV['_'] ? $_ENV['_'] : $_SERVER['_']);
     14:
     15:     // Include configuration file:
     16: require(dirname(PATH_thisScript).'/conf.php');
     17:
     18:     // Include init file:
     19: require(dirname(PATH_thisScript).'/'.$BACK_PATH.'init.php');
     20:
     21:
     22:
     23: # HERE you run your application!
     24:
     25: ?>

- Line 1 will call the PHP binary to parse the script (just like a bash-
  script).

- Line 9 defines "CLI" mode for TYPO3. When this is set browser checks
  are disabled and you can initialize a backend user with the name
  corresponding to the module name you set up in the conf.php file. See
  later.So you  **MUST** set the CLI mode, otherwise you will get
  nowhere.

- Line 13 defines the  *absolute path* to this script! If for some
  reason the environment where the script is run does not offer this
  value in $HTTP\_ENV\_VARS['\_'] you will have to find it elsewhere and
  manuall insert it. There seems to be no general solution for this
  problem.

- Line 16 includes a configuration file build exactly like conf.php
  files for backend modules in extensions. (In fact this script must be
  registered as a backend module)

- Line 19 includes the backend "init.php" file.

After these lines you have a backend environment set up. The browser
check was bypassed and a backend user named like $MCONF['name'] was
initialized. If something failed init.php will exit with an error
message. You can also execute the script with the "status" command
(eg. "/abs/path/to/typo3conf/ext/myext/ myphpshellscript.phpsh
status") to see which user was initialized, which database found and
which path the script runs from. This indicates the success of the
initialization.


conf.php file
"""""""""""""

In the conf.php for the shell script you enter TYPO3\_MOD\_PATH and
backend as usual.

The $MCONF variable is also set with the module name. This must be
prefixed "\_CLI\_" and then a unique module name, eg. based on the
extension key. The value of $MCONF['name'] in lowercase will be the
backend username that is initialized automatically in init.php for
your sessions. This is hardcoded.

An example conf.php file looks like this::

      0:     // DO NOT REMOVE OR CHANGE THESE 3 LINES:
      1: define('TYPO3_MOD_PATH', '../typo3conf/ext/user_fi_io/cronmod/');
      2: $BACK_PATH = '../../../../typo3/';
      3: $MCONF['name'] = '_CLI_userfiio';

The backend user is then named "\_cli\_userfiio":

|img-88|

**Notice:** You must make sure to enter the path of the "shell script
module" in the ext\_emconf.php scripts array (key "module"). If you do
this, the extension manager will automatically fix the paths in the
conf.php file when the extension with your script is installed in
either global / local scopes. This is no different from ordinary
backend modules which need the same attension!


Running the script
""""""""""""""""""

Any script configured like this can be run with the "status" argument
and you will see whether the initialization went well::

   agentk@rock:~$
   agentk@rock:~$ /var/www/typo3/dev/3dsplm_live/typo3conf/ext/user_fi_io/cronmod/index.phpsh status
   Status of TYPO3 CLI script:

   Username [uid]: _cli_userfiio [17]
   Database: t3_3dsplm_live
   PATH_site: /var/www/typo3/dev/3dsplm_live/

   agentk@rock:~$


Natural limitations
"""""""""""""""""""

Since you are not running the script from a web browser all backend
operations that work on URLs or browser information will not produce
correct output. There simply is no URL to get if you ask
"t3lib\_div::getIndpEnv()" for "TYPO3\_SITE\_URL" or so!

You cannot expect to save session data for the authenticated backend
user since there is no session running with cookies either. You should
also remember that all operations done in the script is done with the
permissions of the "\_cli\_\*" user that was authenticated. So make
sure to configure the user correctly. The "\_cli\_" user is not
allowed to be "admin" for security reasons.

