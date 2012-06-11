

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


"locallang.php" files (deprecated)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A "locallang" file looks like this (sysext/lang/locallang\_tca.php):

::

   <?php
   
   $LOCAL_LANG = Array (
       'default' => Array (
           'pages' => 'Page',
           'doktype.I.0' => 'Standard',
           'doktype.I.1' => 'SysFolder',
           'doktype.I.2' => 'Recycler',
           'title' => 'Pagetitle:',
           'php_tree_stop' => 'Stop page tree:',
           'is_siteroot' => 'Is root of website:',
           'storage_pid' => 'General Record Storage page:',
           'be_users' => 'Backend user',
           'be_groups' => 'Backend usergroup',
           'sys_filemounts' => 'Filemount',
       ),
       'dk' => Array (
           'pages' => 'Side',
           'doktype.I.0' => 'Standard',
           'doktype.I.1' => 'SysFolder',
           'doktype.I.2' => 'Papirkurv',
           'title' => 'Sidetitel:',
           'php_tree_stop' => 'Stop sidetræ:',
           'is_siteroot' => 'Siden er websitets rod:',
           'storage_pid' => 'Generel elementlager-side:',
           'be_users' => 'Opdaterings bruger',
           'be_groups' => 'Opdaterings brugergruppe',
           'sys_filemounts' => 'Filmount',
       ),
       'de' => Array (
           'pages' => 'Seite',
           'doktype.I.0' => 'Standard',
           'doktype.I.1' => 'SysOrdner',
           'doktype.I.2' => 'Papierkorb',
           'title' => 'Seitentitel:',
           'php_tree_stop' => 'Seitenbaum stoppen:',
           'is_siteroot' => 'Ist Anfang der Webseite:',
           'storage_pid' => 'Allgemeine Datensatzsammlung:',
           'be_users' => 'Backend Benutzer',
           'be_groups' => 'Backend Benutzergruppe',
           'sys_filemounts' => 'Dateifreigaben',
       ),
   
   ....[lots of other languages defined]...
   
       'sk' => Array (
           'pages' => 'Stránka',
           'doktype.I.0' => 'Štandardná',
           'doktype.I.1' => 'Systémová zložka',
           'title' => 'Titulka stránky',
       ),
       'lt' => Array (
           'pages' => 'Puslapis',
           'doktype.I.0' => 'Standartinis',
           'doktype.I.1' => 'Sisteminis Aplankas',
           'doktype.I.2' => 'Ðiukðlinë',
           'title' => 'Puslapio antraðtë:',
           'php_tree_stop' => 'Stapdyti puslapio medá:',
           'is_siteroot' => 'Ar svetainës ðakninis:',
           'storage_pid' => 'Bendra Puslapio Áraðo saugykla:',
           'be_users' => 'Administravimo pusës vartotojas',
           'be_groups' => 'Administravimo pusës vartotojo grupë',
           'sys_filemounts' => 'Bylø stendas',
       ),
   );
   ?>

So the $LOCAL\_LANG array has the syntax

::

   $LOCAL_LANG[language_key][label_key] = 'label_value';


Alternative locallang-syntax for large translation sets
"""""""""""""""""""""""""""""""""""""""""""""""""""""""

As you can see all available languages are located in the same file!
However if a set of labels is very large it is inefficient to load all
languages into memory when you need only the default plus the current
language to be available (eg. Danish).

Therefore you can split locallang files into a structure with a main
file (locallang\*.php) and sub-files (locallang\*.[langkey].php). An
example is sysext/lang/locallang\_core.php:

::

   <?php
   /**
   * Core language labels. 
   */
   
   $LOCAL_LANG = Array (
       'default' => Array (
           "labels.openInNewWindow" => "Open in new window",
           "labels.goBack" => "Go back",
           "labels.makeShortcut" => "Create a shortcut to this page?",
           "labels.lockedRecord" => "The user '%s' began to edit this record %s ago.",
           "cm.open" => "Open",
   ... [lot of more labels here]....
   
           "cm.save" => "Save",
           "cm.unzip" => "Unzip",
           "cm.info" => "Info",
           "cm.createnew" => "Create new",
   
       ),
       'dk' => "EXT",
       'de' => "EXT",
       'no' => "EXT",
       'it' => "EXT",
       'fr' => "EXT",
       'es' => "EXT",
       'nl' => "EXT",
       'cz' => "EXT",
       'pl' => "EXT",
       'si' => "EXT",
       'fi' => "EXT",
       'tr' => "EXT",
       'se' => "EXT",
       'pt' => "EXT",
       'ru' => "EXT",
       'ro' => "EXT",
       'ch' => "EXT",
       'sk' => "EXT",
       'lt' => "EXT",
   );
   ?>

The string token "EXT" set for all the other languages than "default"
tells the "language" class that another file contains the language for
this language key. For the Danish language this file would be
"sysext/lang/locallang\_core **.dk** .php":

::

   <?php
   /**
   * Core language labels (dk)
   */
   
   $LOCAL_LANG['dk'] = Array (
               "labels.openInNewWindow" => "Åben i nyt vindue",
               "labels.goBack" => "Gå tilbage",
               "labels.makeShortcut" => "Opret genvej til denne side?",
               "cm.open" => "Åbn",
   
   ... [lot of more labels here]....
   
               "cm.save" => "Gem",
               "cm.unzip" => "Unzip",
               "cm.info" => "Info",
               "cm.createnew" => "Opret ny",
   );
   ?>

A requirement is that this "sub-file" sets  *only it's own language
key* (here "dk") in the $LOCAL\_LANG array. Thus simply including this
file after the main file will add the whole "dk" key to the existing
$LOCAL\_LANG array with no need for array merging!

Notice another detail which is a general feature of $LOCAL\_LANG
arrays: The label key 'labels.lockedRecord' is  *not* specified for
the Danish translation. That simply means that the value of the
"default" key (English) will be shown until that value will be added
by the Danish translator!

***Notice: locallang.php files are deprecated! Use locallang-XML files
instead!***

