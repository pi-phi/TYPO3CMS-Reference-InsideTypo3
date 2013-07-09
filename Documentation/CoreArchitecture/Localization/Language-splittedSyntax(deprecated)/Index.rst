.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


"language-splitted" syntax (deprecated)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An old concept called "language-split" has been around for use with
typically table-names, field names etc. in $TCA. This concept is based
on a single string with labels separated by "\|" according to the
number of system languages defined in the TYPO3\_languages constant.
But this approach is now depricated for the future because it is not
very scalable and it's VERY hard to maintain properly. Therefore the
"locallang" concept is required for use anywhere a value is defined to
be "language-splitted" (LS). Instead of specifying a number of labels
separated with "\|" you simply write a code, which refers to a
locallang-file/label inside of that.

Syntax is "LLL:[file-reference of locallang file relative to
PATH\_site]:[key-name]:[extra settings]".

File-reference should be a filename relative to PATH\_site. You can
prepend the reference with "EXT:[extkey]/" in order to refer to
locallang-files from extensions.


((generated))
"""""""""""""

Example:
~~~~~~~~

For the extension "mininews" we have a field called "title". Normally
this would be translated into Danish like this in the $TCA::

      "title" => Array (
                   "exclude" => 0,
                   "label" => "Title:|Titel:",
                   "config" => Array (
                           "type" => "input",
                           "size" => "30",
                           "eval" => "required",
                   )
           ),

But now we would create a file, "locallang\_db.php" in the root of the
extension directory. This would look like this::

   <?php
   $LOCAL_LANG = Array (
           "default" => Array (
                   "tx_mininews_news.title" => "Title:",
           ),
           "dk" => Array (
                   "tx_mininews_news.title" => "Titel:",
           ),
           "de" => Array (
           )
   );
   ?>

As you can see there is an English (red) and Danish (green)
translation. But the German is still missing.

Now, in the $TCA array we change the "language-splitted" label to this
value instead::

      "title" => Array (
                   "exclude" => 0,
                   "label" => "LLL:EXT:mininews/locallang_db.php:tx_mininews_news.title",
                   "config" => Array (
                           "type" => "input",
                           "size" => "30",
                           "eval" => "required",
                   )
           ),

As you can see it has now become a reference to the file
"locallang\_db.php" in the "mininews" extension. Inside this file we
will pick the label "tx\_mininews\_news.title" (this associative key
could be anything you decide. In this case I have just been systematic
in my naming).

Notice how the reference to the locallang file is divided into three
parts separated with a colon, marked with colors corresponding with
the syntax mentioned before: "LLL:[file-reference of locallang file
]:[key-name]:[extra settings]".

The "extra-settings" are currently not used.

