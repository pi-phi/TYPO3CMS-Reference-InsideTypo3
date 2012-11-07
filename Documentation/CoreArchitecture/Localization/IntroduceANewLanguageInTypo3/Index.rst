.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Introduce a new language in TYPO3
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you wish to add a new language to TYPO3, follow these steps:

- First, a 2-char unique language key not yet used (Current Language key
  list: see t3lib/stddb/tbl\_be.php:be\_users:lang) and charset (utf-8
  is default) must be agreed upon.

- Contact a core developer and ask him to add the language key to the
  core. The steps for doing this is defined inside
  t3lib/config\_default.php in a comment just above the definition of
  the constant “TYPO3\_languages”.

- As soon as the language is added to the core you can start translation
  using the extension “llxmltranslate” running on the new core. The
  language pack is automatically created in “typo3conf/l10n/[new
  language key]/”

