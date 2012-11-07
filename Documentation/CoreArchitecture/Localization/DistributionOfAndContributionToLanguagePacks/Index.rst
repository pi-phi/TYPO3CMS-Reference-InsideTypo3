.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Distribution of and contribution to language packs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is still an open question at this point. The basic technical
nature of a language pack is simply that it is a directory in
typo3conf/l10n/ inside of which locallang-xml files are found in
folders according to the position of their main file.

Scheme: “typo3conf/l10n/[lang]/[extkey]/[dir]+[filename]”

This leaves various possibilities of distribution and cooperation:

- **ZIP archives (download)?** Language packs can be distributed as a
  zip file contain translations for any number of extensions.
  Installation of a language pack is no harder than unzipping a file in
  the right directory. Groups of extensions (like the core) can come
  bundled together or extensions can be packed alone. There is currently
  no public download place for such archives.

- **EM support?** One could imagine that support was built into the
  Extension Manager:

  - **Download:** EM could traverse all installed extensions for
    locallang\*.xml files and send a http-request to some repository for
    possible translations located there, then writing them into
    typo3conf/l10n/. EM could even do this transparently based on a
    configuration of which language packs are wanted for the installation.

  - **Upload:** EM could offer to upload local translations of extensions
    to a localization repository. This could be the solution for
    distributed translation of un-common extensions since typically one
    can expect the users of an extension to translate it if not already
    done - and thus, with a click of a button they might wish to share it.

- **CVS?** Putting the whole language pack into CVS might be an idea for
  cooperation on a translation. But maybe there will be too many
  collisions, the language pack in CVS will by time contain translations
  for too many extensions most people don't use and it is not likely
  that all translators have CVS knowledge.

- **rsync?** For both upload and download this could pose a lightweight
  alternative to CVS - especially for multiple translation servers. But
  it suffers many of the problems CVS has.

As a start I would make zip-archives, but my favourite is to integrate
support in EM since:

- It's going to be light weight http upload/download

- EM knows which extensions are relevant on the system and can install
  language packs for extensions transparently as a parallel process to
  installing extensions.

- Allows easy sharing of translations made all over the world (thus an
  answer to the missing “online translation” tool and translations are
  made when needed and with understanding of what is translated)

