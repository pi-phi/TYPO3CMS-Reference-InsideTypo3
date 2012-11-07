.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


How translations are handled by the system
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Here is the basic facts about TYPO3s technology to handle localization
of the backend interface:

- **Default language:** The default language of TYPO3 is English.
  (Please respect this in extensions as well!)

- **Alternative languages:** The list of available system languages is
  defined in the constant TYPO3\_languages (hardcoded/defined in
  config\_default.php). This "list" is two-char identification codes
  representing languages. The code usually reflects a ccTLD related to
  the language but can be any unique 2-char combination.

- **Label files:** All labels for the backend (and frontend) are stored
  in “locallang-XML” (llXML) files located in extensions. They are named
  according to the scheme “locallang\*.xml”. The default labels  *must
  be english!* The system extension “lang” contains labels for the core
  system.

  - *Notice:* "locallang\*.php" files is an old alternative still
    supported but deprecated; They contain the $LOCAL\_LANG array in a PHP
    script which is simply included. Old “locallang.php” files can be
    converted to llXML files using the extension “extdeveval”

- **Localization methods:** The "language" class (from
  sysext/lang/lang.php) contains methods for requesting labels out of
  llXML files in the backend (such as getLL() and sL()). The language
  class also contains an instance of the class "t3lib\_cs" where the
  charsets used for each language are defined. The charset is detected
  by the "template" class and automatically set for the documents in the
  backend.

- **Translation of llXML files:** On a local system this is handled by
  the extension “llxmltranslate”. Unless the llXML files contains inline
  translation or a specific reference to an external file, the
  “llxmltranslate” tool will write the translation to a corresponding
  filename in “typo3conf/l10n/[language key]/[extension key]”
  (recommended).

- **Language packs:** Due to the large amount of languages for TYPO3
  (more than 40) all llXML files in the core and extensions should
  contain  *only* the default english labels. If no entry is found in
  the main file for translations, automatically a translation is looked
  for in “typo3conf/l10n/[language key]/[extension key]”. The directory
  “typo3conf/l10n/[language key]/” is called the “language pack”.

For more detailed information about Frontend localization in TYPO3,
please refer to the document "Frontend Localization Guide"
(doc\_l10nguide).

