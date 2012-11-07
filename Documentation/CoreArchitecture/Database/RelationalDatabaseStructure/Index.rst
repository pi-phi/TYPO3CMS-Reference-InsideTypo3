.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Relational Database Structure
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Despite TYPO3s API for database connectivity which allows you to store
information in eg. XML files instead of MySQL there is still a basic
principle in any case; for TYPO3 internally every “data source” is
expected to work as a flat database table with a number of fields
inside and upon which you can perform queries! In other words; The
DBAL can hide the actual storage mode for TYPO3 totally but internally
TYPO3  *always* expects to select, update, insert and delete the
equivalent of database records stored in tables!

For the rest of this section I will refer to “tables”, “fields” and
“records” as if the data storage truly is a Relational Database
despite that it might be an XML file depending on your current DBAL.


Requirements for TYPO3 managed tables
"""""""""""""""""""""""""""""""""""""

When you want TYPO3 to manage a table for you there are certain
requirements.

- The table must be configured in the global array, $TCA (See “TYPO3
  Core API” for details) - this will tell TYPO3 things like the table
  name, features you have configured, the fields of the table and how to
  render these in the backend, relations to other tables etc.

- You must add at least these fields:

  - “uid” - an auto-incremented integer, PRIMARY key, for the table,
    containing the  *unique* ID of the record in the table.

  - “pid” - an integer pointing to the “uid” of the page (record from
    “pages” table) to which the record belongs.

  - *any other fields you like .... typically at least:*

    - A title field holding the records title as seen in the backend

    - A tstamp field holding the last modification time of the record

    - A sorting order field if records are sorted manually

    - A “deleted” field which tells TYPO3 that the record is deleted (if
      set)


The “pages” table
"""""""""""""""""

One table which has a special status is the “pages” table. This table
is the backbone of TYPO3 as it provides the hierarchical page
structure into which all other TYPO3 managed records are positioned.

You can understand the “pages” table as folders on a hard disc and all
other records (configured in $TCA) as files which can belong to one of
these folders. As a unique identification of any record, “pages”
record or otherwise, the “uid” field contains an integer value. And
for any record the “pid” field is like the “path” in the file system
telling which “page” the record belongs to.

Thus records in the “pages” table has a “pid” value which points to
their “parent page” - the page record they belong to.

If a page (or record from another table) is found in the “Root” they
have the “pid” 0 (zero).

Only admin-users can access records in the root. Also records from
tables can normally only be created on a real page  *or* in the root
(unless configured otherwise).


Other tables
""""""""""""

There are other tables in TYPO3 which are not subject to the uid/pid
scheme as described above. But these tables are not possible to edit
in TYPO3s standard interface (TCEforms/TCEmain). For instance such a
table could be the “sys\_log” table which is automatically written to
each time you update something in TYPO3. Or the “be\_sessions” table
containing user sessions.

Generally:

- If a table is configured in $TCA, then it  *must* have the “uid” and
  “pid” fields as outlined above. Tables configured in $TCA can be
  edited in the backend of TYPO3 and organized in the page tree.

- If a table is not configured in $TCA it means the table is “hidden” to
  the backend user - such tables are controlled by the application logic
  automatically in some way or another.

