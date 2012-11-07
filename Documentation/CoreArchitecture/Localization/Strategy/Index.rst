.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Strategy
^^^^^^^^

Internationalization (i18n) and localization (l10n) issues are handled
by the "language" class included by the "template.php" file and
instantiated as the global variable $LANG in the backend.

The strategy of localization in TYPO3 is to translate all the parts of
the TYPO3 Backend (TBE) interface which are available to everyday
users of the CMS such as content editors, contributors, and to a
certain extend, administrators. However all developer/admin-parts
should remain in English.

The reason for keeping the adminstrator/developer parts in English is
that those parts change and expand too quickly. Further it would be a
huge task to both implement and translate. And the most important
reason is that we want to keep a common vocabulary between developers
in the international TYPO3 developer community. So in fact there are
strong reasons for  *not* translating the  *whole* system into local
languages!

