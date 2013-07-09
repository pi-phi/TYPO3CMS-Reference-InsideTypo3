.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Access Control options
^^^^^^^^^^^^^^^^^^^^^^

A fully initialized backend user has the permissions granted to him by
his own user record and all the user groups he is a member of. These
permissions go into the following conceptual categories:

#. **Access lists** These grant access to backend modules, database
   tables and fields.

#. **Mounts** Parts of the page tree and server file system.

#. **Page permissions** Access to work on individual pages based on the
   user id and group ids.

#. **User TSconfig** A flexible and hierarchical configuration structure
   defined by TypoScript syntax. This typically describes "soft"
   permission settings and options for the user which can be used to
   customize the backend and individual modules.


Online help!
""""""""""""

Before discussing each category, please notice that the online help is
quite extensive and useful as well. Click one of the Help Icons in
relation to either users or groups and you can get a full description
of the table:

|img-36|


Access lists
""""""""""""

Access lists are defined in the user groups and includes

#. **Positivelist of main/submodule.** Which modules appear here depends
   on the access configuration of the individual modules!Access to
   modules is permitted if 1) the module has no restrictions (the $MCONF
   array for the module specifies this) or 2) if the user has the module
   included by the positivelist or 3) is an "admin" user (of
   course).Users must have access to the main module in order to see the
   sub-modules inside listed in the menu. So to have "Web>List" in the
   module menu the user must have access to "Web". Please notice that the
   core module "Tools" is defined to be for "admin" users only and thus
   sub-modules to "Tools" will only appear in the menu for "admin" users.
   **Notice:** As the only one of the access lists, the module list is
   also available in the be\_users records!

#. **Positivelist of tables that are shown in listings (eg. in
   Web>List).** Notice: This list has the list of tables for editing (see
   below) appended. So tables listed for modification need not be
   included in this list as well!

#. **Positivelist of tables that may be edited.** The list includes all
   tables from the $TCA array.

#. **Positivelist of pageTypes (pages.doktype) that can be selected.**

   Choice of pageTypes (doktype) for a page is associated with:

   #. An special icon for the page.

   #. Permitted tables on the page (see `$PAGES\_TYPES global variable
      <#$PAGES_TYPES%7Coutline>`_ ).

   #. If the pageType is

      #. Web-page type (doktype<200, can be seen in 'cms' frontend)

      #. SysFolder type (doktype >=200, can  *not* be seen in 'cms' frontend)

#. **Positivelist of "excludefields" that are not excluded.**
   "Excludefields" are fields in tables that have the "'exclude' => 1"
   flag set in $TCA. If such a field is  *not* found in the list of
   "Allowed Excludefields" then the user cannot edit it! So "Allowed
   Excludefields" adds  *explicit* permission to edit that field.

#. **Explicitly allow/deny field values** This list of checkboxes can be
   used to allow or deny access to specific values of selector boxes in
   TYPO3 tables. Some selectorboxes is configured to have their values
   access controlled. In each case the mode can be that access is
   explicitly allowed or explicitly denied. This list shows all values
   that are under such access control.

#. **Limit to languages** By default users can edit records regardless of
   what language they are assigned to. But using this list you can limit
   the user group members to edit only records localized to a certain
   language.There is also a similar list of languages for each user
   record as well.Technical note; To enable localization access control
   for a table you need to define the field containing the languages.
   This is done with the TCA/"ctrl" directive "languageField". See "TYPO3
   Core API" for more details.

#. **Custom module options** This item can contain custom permission
   options added by extensions.

This screendump shows how the addition of elements to the access lists
can be done for a user group. Notice that the "Include Access Lists"
flag is set - if this is not set, the access lists of a user group is
ignored!

|img-37|

The lists of possible values for access lists are automatically
updated when new tables, fields, modules and doktypes are added by
extensions!

When a user is a member of more than one group, the access lists for
the groups are "added" together.


Mounts
""""""

TYPO3 natively supports two kinds of hierarchical tree structures: The
page tree (Web module) and the folder tree (File module). Each tree is
generated based on the  *mount points* configured for the user. So a
page tree is drawn from the "DB Mount" which is one or more page ids
telling the core from which "root-page" to draw the tree(s). Likewise
is the folder tree drawn based on filemounts configured for the user.

**DB mounts** (page mounts) are easily set by simply pointing out the
page that should be mounted for the user:

|img-38|

If this page, 'Root page A' is mounted for a user, he will see this
page tree:

|img-39|

**Notice:** A DB mount will appear  *only if the page permissions
allows the user read access* to the mounted page (and subpages) -
otherwise no tree will appear!

**File mounts** are a little more difficult to set up. First you have
to create a "Filemount" record in the root:

|img-40|

Then you have to assign that mount to the user or group:

|img-41|

If the filemount was successfully mounted, it will appear like this:

|img-42|

**Notice:** A filemount will work only if the mounted path is
accessible for PHP on the system. Further the path being mounted must
be found within TYPO3\_CONF\_VARS[BE][lockRootPath] (for absolute
paths) or within PATH\_site+TYPO3\_CONF\_VARS[BE][fileadminDir] (for
relative paths) - otherwise the path will not be mounted.

**General notes on mountpoints**

DB and File mounts can be set for both the user and group records.
Having more than one DB or File mount will just result in more than
one mountpoint appearing in the trees. However the backend users
records have two flags which determines whether the DB/File mounts of
*the usergroups* of the user will be mounted as well! Make sure to set
these flags if mountpoints from the member groups should be mounted in
addition to the "private" mountpoints set for the user:

|img-43|

"Admin" users will not need a mountpoint being set - they have by
default the page tree root mounted which grants access to all branches
of the tree. Further the "fileadmin/" dir will be mounted by default
for admin users (provided that TYPO3\_CONF\_VARS[BE][fileadminDir] is
set to "fileadmin/" which it is by default).


Page permissions
""""""""""""""""

Page permissions is designed to work like file permissions on UNIX
systems: Each page record has an owner user and group and then
permission settings for the owner, the group and "everybody". This is
summarized here:

- Every page has an owner, group and everybody-permission

- The owner and group of a page can be empty. Nothing matches with an
  empty user/group (except "admin" users).

- Every page has permissions for owner, group and everybody in these
  five categories:

1 Show: See/Copy page and the pagecontent.

16 Edit pagecontent: Change/Add/Delete/Move pagecontent.

2 Edit page: Change/Move the page, eg. change title, startdate,
hidden.

4 Delete page: Delete the page and pagecontent.

8 New pages: Create new pages under the page.

(Definition: "Pagecontent" means all records (except from the
"pages"-table) related to that page.)

Page permissions are set and viewed by the module "Access":

|img-44|

Editing permissions for a page is done by clicking the edit icon:

|img-45|

Here you can set owner user/group and the permission matrix for the
five categories / owner, group, everybody. Notice that permissions can
be set recursively if you select that option in the selector box just
above the "Save"/"Abort" buttons.

A user must be "admin"  *or* the owner of a page in order to edit its
permissions.

**New pages and records.**

When a user creates new pages in TYPO3 they will by default get the
creating user as owner. The owner group will be set to the  *first
listed user group* configured for the users record (if any) (available
in $BE\_USER->firstMainGroup). These defaults can be `changed through
Page TSconfig <../Sites/typo3/doc_core_tsconfig/doc/manual.sxw#Page%20
TSconfig%7Coutline>`_ .

If you wish to change the default values user/group/everybody it can
be done by TYPO3\_CONF\_VARS[BE][defaultPermissions] (please read
comments in the source code of config\_defaults.php).


User TSconfig
"""""""""""""

User TSconfig is a hierarchical configuration structure entered in
plain text TypoScript. It can be used by all kinds of applications
inside of TYPO3 to retrieve customized settings for users which
relates to a certain module or part. The options available is
described in the `document TSconfig <../Sites/typo3/doc_core_tsconfig/
doc/manual.sxw#User%20TSconfig%7Coutline>`_ .

A good example is to look at the script 'alt\_main.php' in which the
shortcut frame is displayed in the frameset only if the User TSconfig
option "options.shortcutFrame" is true::

   if ($BE_USER->getTSConfigVal('options.shortcutFrame'))    {....

Likewise other scripts and modules in TYPO3 is able to acquire a value
from the User TSconfig field.

So if we wanted to enable the shortcut frame for a user we would set
the TSconfig field of the user record (or any member group!) like
this:

|img-46|

... or alternatively this (which is totally the same, just another way
of entering values in TypoScript syntax):

|img-47|

**Precedence order of TSconfig:**

The TSconfig of the users  *own* record (be\_users) will be included
*last* so any option in the "be\_users" TSconfig field can override
options from the groups or the default TSconfig which was previously
set.

Further notice that the TYPO3\_CONF\_VARS[BE][defaultUserTSconfig]
value can be configured with default TSconfig for all be\_users.

"Admin" users further has a minor set of default TSconfig as well::

   admPanel.enable.all = 1
   setup.default.deleteCmdInClipboard = 1
   options.shortcutFrame=1

