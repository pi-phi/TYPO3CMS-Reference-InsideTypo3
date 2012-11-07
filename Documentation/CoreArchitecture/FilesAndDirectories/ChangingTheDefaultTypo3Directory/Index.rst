.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Changing the default “typo3/” directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default TYPO3 is administrated from the directory “typo3/”. You can
change (rename) that so the backend is available from another
directory, eg. “my\_typo3\_admin\_dir/”. But the frontend and backend
is tied together in some ways that mean you'll have to change parts of
the source code. That is relatively easy if you follow these
guidelines:

- Rename the “typo3/” dir/softlink to “my\_typo3\_admin\_dir/”. Notice
  that the backend directory must always be a sub directory to the
  website (extensions inside + frontend edit relies on the backend to be
  there). Further it cannot be a sub-sub-directory either! (This will
  work only partially and is currently not intended to be fixed).

- Search for the string 'define("TYPO3\_mainDir"'. At least four scripts
  will be found: typo3/sysext/cms/tslib/index\_ts.php (the index.php
  file), typo3/sysext/cms/tslib/showpic.php, t3lib/thumbs.php and
  typo3/init.php. With each instance change the constant definition from
  “typo3/” to “my\_typo3\_admin\_dir/”.

- Any local extensions (those installed in typo3conf/ext/) that has
  backend modules in them (those with conf.php files) MUST have their
  $BACK\_PATH definition in the conf.php file changed! If they are
  installed by the extension manager everything should be fine, but if
  not, you must change manually. You will receive an error something
  like this:Warning: Failed opening '../../../../typo3/init.php' for
  inclusion...

- Rarely: The extension “direct\_mail” has two cron-scripts,
  dmailerd.phpcron and returnmail.phpsh. They have “typo3/” hardcoded as
  admin directory as well. If you use these scripts, you will have to
  change that too.

- Finally you should remove the “temp\_CACHED\_ps\*” files found in
  typo3conf/ before you test the new settings. Those will be re-
  generated with adjusted paths on the first executing of a TYPO3
  script. On UNIX systems something like this will do the trick::

     rm typo3conf/temp_CACHED_ps*

