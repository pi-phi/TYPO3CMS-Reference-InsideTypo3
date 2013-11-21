.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Other options
^^^^^^^^^^^^^

Finally there are a few other options for users and groups which are
not yet mentioned and requires a short note. Still remember that the
Context Sensitive Help available through the tiny help icons will also
provide information for each option!


Backend Users
"""""""""""""

|img-48|

- **Default language** The backend system language selected for the user
  *by default* . As soon as the user has been logged in once this value
  will  *no longer have any effect* since the value of this field is
  transferred to the internal User Configuration array ->uc of the user
  object and the user will himself be able to change this value from the
  extension "Setup" (User > Setup) if available to him.Only if the
  contents of the "uc" field in the user record is cleared (for example
  by the Install Tool), then this value will be re-inserted as the
  default language.

- **Fileoperation permissions** These permissions take effect in the
  `file part of TCE (TYPO3 Core Engine)
  <#Files:%20t3lib_extFileFunctions%20basics%7Coutline>`_ where
  management of files and folders within the filemounts of a user is
  controlled.

- **General options** You can at any time disable a user or apply a time
  interval where the user is allowed to be authenticated. Sessions will
  be ended immediately if the disabled flag is set or the start or stop
  times are exceeded.

- **Lock to domain** (Not shown in screenshot) Setting this to for
  example "www.my-domain.com" will require a user to be logged in from
  that domain. Very useful in databases with multiple sites/domains
  since this will prevent users from logging in from the domains of
  other sites in the database. If a user logs in from another domain
  than the one associated with his page tree it doesn't give him
  *access* to that site though - but it surely  *feels* like a security
  hole although it is not. But setting this value you can force the user
  to be authenticated only from a certain URL.


Backend Groups
""""""""""""""

|img-49|

- **Disable** Setting this flag will immediately disable the group for
  all members

- **Lock to domain** Setting this to for example "www.my-domain.com"
  will require a user to be logged in from that domain if membership of
  this group should be gained. Otherwise the group will be ignored for
  the user.

- **Include Access Lists** If this options is set, the access lists - as
  discussed earlier - are enabled.

- **Hide in lists** This flag will prevent the group from appearing in
  listings in TYPO3. This includes modules like Web > Access and the Task
  Center (listing groups for messages, todos etc.)

- **Sub Groups** Assigns sub-groups to this group. Sub-groups are
  evaluated before the group including them. If a user has membership of
  a group which includes one or more sub-groups then the subgroups will
  also appear as member groups for the user.

- **Description** Any note you want to attach which can help you
  remember what this group was made for: Special role? Special purpose?
  Just put in a description.

