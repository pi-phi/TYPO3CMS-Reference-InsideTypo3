

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


((generated))
^^^^^^^^^^^^^

Basic facts about Context Sensitive Help
""""""""""""""""""""""""""""""""""""""""

These are some basic facts about how CSH works:

- Context Sensitive Help (CSH) labels are stored in locallang files
  inside of extensions, typically in a main file with English and sub-
  files with the individual languages.

- The CSH locallang files are typically named 'locallang\_csh\_\*.php'
  or "locallang\_csh\_\*.xml"

- They are translated as any other locallang file on typo3.org (for
  "php" versions) or by the backend module in the extension
  "llxmltranslate" (for the recommended "xml" version)!

- CSH labels can override or add themselves to existing values thus
  allowing for local, customized help. Very flexible.

