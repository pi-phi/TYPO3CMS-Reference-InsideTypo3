.. include:: Images.txt

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


Basic Core Installation Summary
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

So lets sum up what we have now:


File structure
""""""""""""""

These are themain directories of interest:

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Directory
         Directory
   
   Content
         Content


.. container:: table-row

   Directory
         t3lib/
   
   Content
         TYPO3 libraries and core database setup (t3lib/stddb/)


.. container:: table-row

   Directory
         typo3/
         
         *(shared between all websites)*
   
   Content
         Source code of the TYPO3 administration backend. Can be symlink'ed to
         the "typo3\_src" source code located elsewhere.
         
         Most directories can be write protected except as noted below


.. container:: table-row

   Directory
         ext/
         
         sysext/
   
   Content
         Directories containing extensions.
         
         ext/ is for "global" extensions and sysext/ for "system" extensions.
         Both types are available for all installations sharing this source
         code.
         
         The difference is that  *global* extensions might be missing from the
         distributed source code (meant to be updated by the EM) while the
         *system* extensions are "permanent" and will always be a part of the
         distributed source. Further you cannot update the system extensions
         unless you set a certain configuration flag in TYPO3\_CONF\_VARS
         
         **NOTE: In case you want to allow the Extension Manager to update
         global and system extensions you must also allow writing to "ext/" and
         "sysext/". Install Tool will warn you.**


.. container:: table-row

   Directory
         gfx/
   
   Content
         Various graphical elements


.. container:: table-row

   Directory
         install/
   
   Content
         Contains the Install Tool starter-script. Basically this is an index
         .php-script which initializes a constant that - if defined - will
         launch the Install Tool.
         
         **NOTE: Make sure to properly secure access to the Install Tool!**


.. container:: table-row

   Directory
         mod/
   
   Content
         Backend modules. Reflects the old concept of modules and submodules
         from before extensions hit the scene in summer 2002. Today it contains
         mostly placeholders, "host modules" and default core modules like the
         Extension Manager (mod/tools/em).


.. container:: table-row

   Directory
         typo3conf/
         
         *(specific for each website)*
   
   Content
         Local directory with configuration and local extensions.
         
         Can be used for additional user defined purposes as you like.
         
         Must be writeable by PHP.
         
         **localconf.php:**
         
         Main configuration of the local TYPO3 installation. Database username,
         password, install tool password etc.
         
         **temp\_CACHED\_xxxxxx\_ext\_localconf.php**
         
         **temp\_CACHED\_xxxxxx\_ext\_tables.php:**
         
         Auto-generated cache-files of "ext\_localconf.php" and
         "ext\_tables.php" files from all loaded extensions. Can be deleted at
         any time and will be automatically written again.


.. container:: table-row

   Directory
         typo3temp/
         
         *(specific for each website)*
   
   Content
         For temporary files.


.. container:: table-row

   Directory
         uploads/
         
         *(specific for each website)*
   
   Content
         For storage of files attached to database records as managed by the
         TCE. Strictly this directory (and subdirectories) is only needed if
         it's configured in $TCA.
         
         Also used by default for images inserted into the RTE.


.. ###### END~OF~TABLE ######

Basically we completed these steps to create the files and folders of
a bare-bone TYPO3 core installation:

- Create symlink to the t3lib/ directory  *(shared)*

- Create symlink to the backend administration directory, typo3/
  *(shared)*

- Create directories typo3conf/, uploads/, typo3temp/  *(specific)*

- Create typo3conf/localconf.php file and add a minimum of configuration
  to get started.  *(specific)*


Notice on temp\_CACHED-files in typo3conf/
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are two (sometimes more) files which we didn't create ourselves;
the cached "temp\_CACHED\_xxxxxx\_ext\_localconf.php" and
"temp\_CACHED\_xxxxxx\_ext\_tables.php". These two files are
automatically compiled from the currently loaded extensions and
written to disk. If you look into the files you can see that they are
just scripts automatically collected from the loaded extensions, then
concatenated and written to disk. This concept improves parsing  *a
lot* since it make it possible to include one file (the cached file)
instead of maybe 50 files from different locations.

**WARNING:** If you install an extensions which has a parsing error in
either the "ext\_localconf.php" file or "ext\_tables.php" file you
will most likely be unable to use either frontend, backend or Install
Tool before this problem is fixed. You fix the problem by using a
shell or ftp to 1) edit localconf.php file, removing the "bad"
extension key from the list of installed extensions, then 2) remove
the cached files and 3) hit the browser again (cached files will be
rewritten, but without bad files). Of course the long term solution is
to fix the parsing error...


typo3conf/localconf.php
"""""""""""""""""""""""

The file contained

#. A password so we could enter the Install Tool

#. An extension list with only the "install" extension set (Install
   Tool). Normally there are a long list of default extensions listed.

#. A required extensions list set to only the "lang" extension (all the
   labels for the backend interface). (Required extensions cannot be
   disabled by the EM)

#. Database setup information, including the database name (added by
   Install Tool after database creation).


Backend features
""""""""""""""""

Looking into the backend of our "bare bone" install this is what we
see:

|img-11|

Notice how few modules are available!  *This* is the default set of
features which exists in what we call  *the core* of TYPO3! If you go
to the Extension Manager (EM) and enable "Shy extensions" you can see
that only the "lang" and the "install" extensions are there. Even the
Install Tool is an extension that can be disabled.


Database structure
""""""""""""""""""

After these steps you have also created a database and populated it
with a default set of tables. So how did the Install Tool know which
tables were needed? Simple answer: The Install Tool simply reads the
core sql-file (t3lib/stddb/tables.sql) plus similar files for every
installed extension ([extension\_dir]/ext\_tables.sql) and adds it all
together into a requirement for the fields and keys of the tables!
Thus the database will always have the correct number of tables with
the correct number and types of fields!

**NOTICE:** You cannot necessarily pass these sql-files directly to
MySQL! If you look into the file t3lib/stddb/tables.sql you can find a
table definition like this:

::

   #
   # Table structure for table 'cache_hash'
   #
   CREATE TABLE cache_hash (
     hash varchar(32) DEFAULT '' NOT NULL,
     content mediumblob NOT NULL,
     tstamp int(11) unsigned DEFAULT '0' NOT NULL,
     ident varchar(20) DEFAULT '' NOT NULL,
     PRIMARY KEY (hash)
   );

And in some extension ( *myextension* ) you could find something along
these lines:

::

   #
   # Table structure for table 'cache_hash'
   #
   CREATE TABLE cache_hash (
     tx_myextension_additionalfield varchar(20) DEFAULT '' NOT NULL,
   );

The first "CREATE TABLE" query will execute just fine if you "pipe" it
into MySQL directly, but the second one will not! And it was not
intended to!

The reason is that IF  *myextension* is installedthen the Install Tool
will read both files and  *automatically* compile the final query into
this:

::

   CREATE TABLE cache_hash (
     hash varchar(32) DEFAULT '' NOT NULL,
     content mediumblob NOT NULL,
     tstamp int(11) unsigned DEFAULT '0' NOT NULL,
     ident varchar(20) DEFAULT '' NOT NULL,
     tx_myextension_additionalfield varchar(20) DEFAULT '' NOT NULL,
     PRIMARY KEY (hash)
   );

If we install the "phpmyadmin" extension we can browse the database
tables from the backend:

|img-12|

As we can see the number of required tables for a minimum install of
TYPO3 is really just 13 tables!

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Tablename
         Tablename
   
   Description
         Description


.. container:: table-row

   Tablename
         pages
   
   Description
         The "directory tree" (page tree) backbone of TYPO3s database
         organization concept.


.. container:: table-row

   Tablename
         be\_groups
         
         be\_users
         
         be\_sessions
         
         sys\_filemounts
   
   Description
         Tables with backend user groups and users plus a table for storing
         their login sessions.
         
         sys\_filemounts are used to associate users/groups with filepaths
         where they can upload and manage files.


.. container:: table-row

   Tablename
         cache\_hash
         
         cache\_imagesizes
   
   Description
         Multi purpose table for storing cached information (cache\_hash) and
         cache table for image sizes of temporary files.


.. container:: table-row

   Tablename
         sys\_be\_shortcuts
   
   Description
         Stores the shortcuts users can create in various backend modules


.. container:: table-row

   Tablename
         sys\_history
   
   Description
         Contains the history/undo data


.. container:: table-row

   Tablename
         sys\_lockedrecords
   
   Description
         Keeps track of "locked records" - basically who is editing what at the
         moment.


.. container:: table-row

   Tablename
         sys\_log
   
   Description
         Backend log table - logs actions like file management, database
         management and login


.. container:: table-row

   Tablename
         sys\_language
   
   Description
         System languages for use in records that are localized into certain
         languages.


.. container:: table-row

   Tablename
         sys\_workspace
   
   Description
         System workspaces for editing of content in “offline” mode or in
         projects.


.. ###### END~OF~TABLE ######

Even if you look at the "pages" you will quickly see that the core
pages table miss a lot of the fields and features applied to it when
used under "CMS conditions". All meta-fields are gone, all content
management related fields are gone. Left is only a set of general
purpose options:

|img-13|


The point?
""""""""""

And the point is; TYPO3s inner identity is that of a  *framework*
which  *by additional extensions* can be dressed up for the purpose it
needs to fulfil. 99% of all people who are using TYPO3 will see the
"dressed up version" designed for web content management. However my
claim is that if you really want to understand TYPO3 you must get down
to the core, to the principles which lay the foundation of it all. If
you have a firm grip on these central principles then you will quickly
understand or be able to analyze how each extension on top of it
works. And you as a developer will be able to help the continual
development along consistent lines of thought.

Welcome Inside of TYPO3!

\- kasper

