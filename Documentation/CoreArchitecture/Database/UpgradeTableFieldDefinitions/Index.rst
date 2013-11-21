.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Upgrade table/field definitions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When you upgrade to newer versions of TYPO3 or any extension in TYPO3
the requirements to the database tables and fields might have changed.
However TYPO3 handles this automatically. If a new field or table has
been added or changed the Install Tool in TYPO3 will detect that and
warn you. When you install extensions, you will be warned as a part of
the process when the extension is installed. When you upgrade the
TYPO3 core source code you will have to manually trigger the
validation functions inside the Install Tool:

|img-89|

The step you should always take is to click the "COMPARE" link for
"Update required tables" in the Install Tool. Now TYPO3 will search
for the file "ext\_tables.sql" in  *all* installed extensions, add
them together with the core requirements (t3lib/stddb/tables.sql) and
take that as the complete expression of the database structure TYPO3
requires. Then TYPO3 will ask the database for the actual table /
field structure and compare them. Any fields that has been added or
changed will be shown and new tables can be created in the interface
that pops up:

|img-90|

A single click on a button in the bottom of the screen will carry out
these changes for you!

As you can also see you will be told if tables or fields are not used
any more. You can also choose to delete those if you like but it is
not vital for the system to function correctly.

If the database matches exactly with the combined requirements of core
and extensions you will see this message:

|img-91|

The class that contains code for comparing SQL files with the database
is "t3lib/class.t3lib\_install.php".


The ext\_tables.sql files
"""""""""""""""""""""""""

Each extension might provide requirements for tables and/or fields in
the database. This is done from the ext\_tables.sql file. But the file
is not (always) a valid SQL dump. In this case taken from the
extension "TemplaVoila" you can see a full table definition at first.
This can be piped to MySQL and a new table will be created.

But the second "CREATE TABLE" definition is incomplete. This is on
purpose because it actually adds four new fields to the already
existing table "tt\_content".

When the Install Tool reads the "ext\_tables.sql" files it will
automatically read these four lines and add them to the previously
defined requirements for the "tt\_content" table. ::

   #
   # Table structure for table 'tx_templavoila_datastructure'
   #
   CREATE TABLE tx_templavoila_datastructure (
           uid int(11) unsigned DEFAULT '0' NOT NULL auto_increment,
           pid int(11) unsigned DEFAULT '0' NOT NULL,
           tstamp int(11) unsigned DEFAULT '0' NOT NULL,
           crdate int(11) unsigned DEFAULT '0' NOT NULL,
           cruser_id int(11) unsigned DEFAULT '0' NOT NULL,
           deleted tinyint(4) unsigned DEFAULT '0' NOT NULL,
           title varchar(60) DEFAULT '' NOT NULL,
           dataprot mediumtext NOT NULL,
           scope tinyint(4) unsigned DEFAULT '0' NOT NULL,
           previewicon tinytext NOT NULL,

           PRIMARY KEY (uid),
           KEY parent (pid)
   );

   #
   # Table structure for table 'tt_content'
   #
   CREATE TABLE tt_content (
           tx_templavoila_ds varchar(100) DEFAULT '' NOT NULL,
           tx_templavoila_to int(11) DEFAULT '0' NOT NULL,
       tx_templavoila_flex mediumtext NOT NULL,
       tx_templavoila_pito int(11) DEFAULT '0' NOT NULL
   );


The upgrade process
"""""""""""""""""""

More information about the process of upgrading TYPO3 can be found in
the document :ref:`"Installation and Upgrade Guide"
<t3install:upgrade>` .

