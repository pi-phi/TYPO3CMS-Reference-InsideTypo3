.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Character sets
^^^^^^^^^^^^^^

Currently, local charsets are used  *by default* inside TYPO3. However
it is highly recommended to set
$TYPO3\_CONF\_VARS['BE']['forceCharset'] = "utf-8" which will force
the backend to run in utf-8 regardless of "native" charset. Forcing
the charset to "utf-8" also means that all content in the database
will be managed in "utf-8" and you might corrupt existing data if you
set it after having added content in another charset.

