.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Character sets
^^^^^^^^^^^^^^

Since TYPO3 4.5, character sets other than utf-8 were deprecated and the
default character set to work with internally was set to utf-8 in
$TYPO3\_CONF\_VARS['BE']['forceCharset'].

Since version 4.7, TYPO3 only supports utf-8 as the character set to work with
internally. The setting $TYPO3\_CONF\_VARS['BE']['forceCharset'] is now
hardcoded to "utf-8". If in your database, your content is not yet stored in
utf-8, you must convert it to utf-8. More information are available `on our
wiki page on UTF-8 support`_.

.. _on our wiki page on UTF-8 support: http://wiki.typo3.org/UTF-8_support

