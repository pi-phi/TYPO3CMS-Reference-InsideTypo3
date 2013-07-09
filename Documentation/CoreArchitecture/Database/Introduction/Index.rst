.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Introduction
^^^^^^^^^^^^

TYPO3 is centered around a RDB - a relational database. This database
has historically been MySQL and until version 3.6.0 of TYPO3 MySQL
calls were hardcoded into TYPO3.

Today you can use other databases thanks to a wrapper class in TYPO3,
"t3lib\_DB". This class implements a simple database API plus mysql-
wrapper function calls which gives us the following features:

- Backwards compatibility with old extensions

- Easy migration to database abstraction for old extensions

- Offering the opportunity of applying a DBAL (DataBase Abstraction
  Layer) as an extension (thus offering connectivity to other databases
  / information sources)

  - A DBAL can simply implement storage in other RDBs

  - Or it could be a simulation of a RDB while actually storing
    information totally different, like in XML files.

  - Or you create a simulation of the "be\_users" table while looking up
    information in LDAP instead.

- Keeping a minimal overhead (in the range of 5%) for plain MySQL usage
  (which is probably what most TYPO3 based solutions is running anyway)

In other words; TYPO3 is optimized for MySQL but can perform with any
information source for which someone will write a "driver". Such
drivers can easily be implemented as extensions thus offering other
developers a chance to implement a full blown DBAL for TYPO3 in an
extension - or for the local TYPO3 project this can offer improvised
implementation of eg. XML database sources or whatever.

