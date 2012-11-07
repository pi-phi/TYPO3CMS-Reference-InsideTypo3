.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


What are extensions
^^^^^^^^^^^^^^^^^^^

First of all this is only a short description of extensions; For a
more detailed description of extension, please see the `Extension API
section in "TYPO3 Core API" <#TYPO3%20Extension%20API%7Coutline>`_ .

An "extension" in relation to TYPO3 is a set of files/scripts which
can integrate themselves with TYPO3s core through an API an thus
seemlessly extend the capabilities of TYPO3.

These are the basic properties of extensions:

- All files contained within a single directory

- Easily installed/removed/exchanged

- Has a unique key (extension key) used for naming of all elements
  (variables, database tables, fields, classes etc.).

- Can interact with any part of the system. If not through the available
  APIs, ultimately (almost) any class in TYPO3 can be extended with full
  backwards compatibility maintained.


Where are extensions located?
"""""""""""""""""""""""""""""

|img-25|

Extensions can be installed in three locations:

#. typo3/ext/: Global extensions. A part of the source code directory.
   Available to all TYPO3 installations sharing the same sourcecode. Is
   not  *necessarily* available! You can remove or add extensions here
   and some source distributions will not contain the ext/ directory with
   global extensions (in which case you will have to add them yourself
   from TER).

#. typo3/sysext/: System extensions. Just like global extensions: A part
   of the source code directory. But the system extensions are  *always*
   distributed with the source code so you can depend on them being
   there. Further you generally don't need to upgrade system extensions
   manually as they are upgraded with new source code releases. System
   extensions carry a special status of being officially endorsed by the
   TYPO3 system and they are required to match the quality of the core
   code regarding the standards set out in the TYPO3 Coding Guidelines.

#. typo3conf/ext/: Local extensions: Only available to the local TYPO3
   installation. This is the typical location for most extensions which
   are installed on a per-project basis since the extension is used in
   only this one case. Also the position for user defined extensions.


What can they change?
"""""""""""""""""""""

Extensions can change practically anything in TYPO3. The concept is
very capable since it was created to add limitless power to TYPO3
without having to directly change the core. As such extensions will
make it possible for TYPO3 to be a true framework for just any
application you can imagine. Installing one set of extensions will
make TYPO3 one application - installing another set of extension will
make TYPO3 another application. And the core is thus a basic set of
modules, an Extension Manager and an API provided for the extensions
so they can use core features right away.

Although the basic rule is "anything is possible" this is at least a
partial list of features provided by extensions:

- Addition of database tables and fields to existing tables.

- Addition of tables with static information

- Addition of TypoScript static template files or adhoc snippets

- Addition of backend skins

- Addition of frontend plugins of any kind

- Addition of backend modules of any kind

- Addition of click-menu items (context sensitive menus)

- Addition of Page and User TSconfig

- Addition of configuration values

- Extension of any class in the system

... and of course all kinds of combinations.

