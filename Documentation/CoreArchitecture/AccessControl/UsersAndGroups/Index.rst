.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Users and groups
^^^^^^^^^^^^^^^^

TYPO3 features an access control system based on users and groups.


Users
"""""

Each user of the backend must be represented with a single record in
the table "be\_users". This record contains the username and password,
other meta data and some permissions settings.

|img-32|

The above screenshot shows a part of the editing form for the backend
user with uid=2 and username='guest'. The user is a member of the
group 'guest\_group' and has English as the default language.


Groups
""""""

Each user can also be a member of one or more groups (from the
be\_groups table) and each group can include sub-groups. Groups
contain the main permission settings you can set for a user. Many
users can be a member of the same group and thus share permissions.

When a user is a member of many groups (including sub-groups) then the
permission settings are added together so that the more groups a user
is a member of, then more access is granted to him.

|img-33|

This screenshot shows the field for the group title - there are many
more fields for access settings! See the following pages.


The "admin" user
""""""""""""""""

A user can have a single flag set called "Admin". If this is set the
user doesn't need any further access settings since this will grant
TOTAL access to the system in the backend! There can be no real
limitations to what an "admin" user can do! Like the "root"-user on a
UNIX system.

All systems must have at least one "admin" user and most systems
should have  *only* one "admin" user. It should probably be the
developer with the total understanding of the system. Not even "super
users" should be allowed "admin" access since that will most likely
grant them access to more than they need.

Admin-users are easily recognized since they have a red icon.

|img-34|


A level between "admin" users and ordinary users
""""""""""""""""""""""""""""""""""""""""""""""""

It has often been requested to have more access levels between "admin"
users and normal users in a system. This is particularly true when
TYPO3 works as a CMS and some users should have access to TypoScript
templates in the Web > Template module.

The reason why this is not possible to allow for normal users is that
it fails the "PHP-execution criteria". By allowing users to alter
TypoScript values in frontend templates you also offer them a way to
execute custom PHP code on the server - which in turn means they can
create a full "admin" account for themselves easily.

The "PHP-execution criteria" is typically the reason why a certain
level of access is not possible to grant non-admin users - simply
because they may be able to escalate their rights if they could.


Location of users and groups
""""""""""""""""""""""""""""

Since both backend users and backend groups are represented by records
in the database they are edited just as any other record in the
system. However backend users and groups are configured to exist
*only* in the root of the page tree where  *only* "admin" users have
access:

|img-35|

This screenshot shows two backend users, "guest" (regular user - blue)
and "admin" (admin user - red), located in the root of the page tree
together with the group "guest\_group". To edit the users and groups
just click the icon and select "Edit" as you would edit any other
record. Even creation of new users and groups is done with similar
basic tools of the TYPO3 core.

Records located in the page tree root are identified by having their
"pid" fields set to zero. The "pid" field normally contains the
relation to the page where a record belongs. Since no pages can have
the id of zero, this is the id of the root. Notice that only "admin"
users can edit records in the page root! If you want non-admin users
(eg. a super user) to create new users, please install the
"sys\_action" extension which supplies an "action" for doing just
that.

