.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


More about File Mounts
^^^^^^^^^^^^^^^^^^^^^^

File mounts require a little more description of the concepts provided
by TYPO3.

First lets discuss the relative and absolute filemounts again. In the
follow example we use two filemount records which are created in the
root:

|img-50|

These have been applied to a user or a member group for a user.


Relative
""""""""

Relative filemounts are paths which are mounted relative to the
directory given by $TYPO3\_CONF\_VARS['BE']['fileadminDir']. This
value is by default set to "fileadmin/" which is also a directory
found on most TYPO3 installations.

|img-51|

In this example the folder "fileadmin/webfolder/" is mounted for a
user. "fileadmin/webfolder/" is  *always* relative to the constant
PATH\_site.

If you want to make this filemount work it requires - of course - that
the path "fileadmin/webfolder/" is in fact present below the
PATH\_site. That is not yet the case if you did the core installation
from the introduction chapter of this document. So the following steps
will prepare the directory for use from scratch (on a UNIX box)::

   [root@T3dev coreinstall]# mkdir fileadmin/
   [root@T3dev coreinstall]# mkdir fileadmin/webfolder/
   [root@T3dev coreinstall]# chown httpd.httpd fileadmin/ -R

("mkdir" means "Make Directory", "chown" means "Change Owner". They
are UNIX commands)

Notice how ownership of the created folders is changed to "httpd"
which is the UNIX-user that Apache on this particular server executes
PHP-scripts as.

If $TYPO3\_CONF\_VARS['BE']['fileadminDir'] is false, no relative
filemounts are allowed.

Remember that "admin" users will have the
$TYPO3\_CONF\_VARS['BE']['fileadminDir'] path mounted by default - all
other users requires a "Filemount" record to be created and added to
their user record/member groups.

Since relative filemounts are located within the document root of the
website, the URL of the mounted "fileadmin/webfolder/" would be for
example "http://www.my-typo3-site.org/fileadmin/webfolder/" provided
that "http://www.my-typo3-site.org/" is the domain of the frontend.


Absolute
""""""""

The alternative to relative filemounts - which enables people to
upload files into the webspace of the site! - is absolute filemounts.
These can be mounted "internally" on the server and thus manage files
which are not available from a URL. The requirement for this is that
$TYPO3\_CONF\_VARS['BE']['lockRootPath'] is set to match the  *first
part* of any absolute path being mounted.

|img-52|

In this case "/my\_absolute\_path/another\_dir/" is mounted.

Before this will work we will have to configure 'lockRootPath'. In
typo3conf/localconf.php, enter::

   $TYPO3_CONF_VARS['BE']['lockRootPath']='/my_absolute_path/';

Also create the directories::

      mkdir /my_absolute_path
           mkdir /my_absolute_path/another_dir/
           chown httpd.httpd /my_absolute_path/ -R

**Safe mode restrictions**

Notice that safe\_mode and other security restrictions might prevent
PHP from working on files outside the document root and thus prevent
absolute filemounts from working! See the "Installation and Upgrade
Guide" for more details on :ref:`how to configure PHP <t3install:php>`
environments.


Home directories
""""""""""""""""

TYPO3 also features the concept of "home directories". These are paths
that are automatically mounted if they are present at a path
configured in TYPO3\_CONF\_VARS. Thus they don't need to have a file
mount record representing them - they just need a properly named
directory to be present. Home directories are nice if you have many
users which need individual storage space for their uploaded files or
if you want to supply FTP-access to TYPO3 - then the safer option is
to allow users FTP-access to a non-web area on the server. Then users
can access those files from TYPO3.

The parent directory of user/group home directories is defined by
$TYPO3\_CONF\_VARS['BE']['userHomePath'] and
$TYPO3\_CONF\_VARS['BE']['groupHomePath'] respectively. In both cases
the paths  *must be* within the path prefix defined by
$TYPO3\_CONF\_VARS['BE']['lockRootPath']! Otherwise they will not be
mounted (as with any other absolute path).

Lets configure::

   $TYPO3_CONF_VARS['BE']['lockRootPath'] ='/my_absolute_path/';
   $TYPO3_CONF_VARS['BE']['userHomePath'] ='/my_absolute_path/users/';
   $TYPO3_CONF_VARS['BE']['groupHomePath']='/my_absolute_path/groups/';

Lets create::

   mkdir /my_absolute_path/users/
   mkdir /my_absolute_path/users/2/
   mkdir /my_absolute_path/users/1_admin/
   mkdir /my_absolute_path/groups
   mkdir /my_absolute_path/groups/1
   chown httpd.httpd /my_absolute_path/ -R

These lines create

- The parent directory for user home dirs, /my\_absolute\_path/users

- The parent directory for group home dirs, /my\_absolute\_path/groups

- A  *home directory* for the "be\_group" with uid=1;
  /my\_absolute\_path/groups/1

- A home directory for the "be\_user" with uid=1/username="admin";
  /my\_absolute\_path/users/1\_admin/

- A home directory for the "be\_user" with uid=2/username=?;
  /my\_absolute\_path/users/2/

Notice how one user home dir is named "1\_admin" where "1" is the user
uid and "admin" is the username. When user dirs are mounted TYPO3
first looks for a directory named "[uid]\_[username]", then - if not
found - for a directory named "[uid]". So the username is optional and
*can* be a help if you want to identify a users directory without
having to look up his uid. However changing the username will break
the link to the directory of course.

After having created these directories and configured
TYPO3\_CONF\_VARS to set them up, the folder tree looks like this for
the admin-user of the core\_install:

|img-53|

Here are some comment to the screenshot:

#. "fileadmin/" is the $TYPO3\_CONF\_VARS['BE']['fileadminDir'] directory
   *mounted by default* for "admin" users!

#. This is the users  *private* home directory in
   "/my\_absolute\_path/users/1\_admin/". Only the user "admin" has
   access to this directory.

#. This is the "public" home directory that belongs to the group
   "guest\_group" (uid=1). This is mounted because the "admin" user has
   been assigned membership of the "guest\_group"! Other users with
   membership of this group will have access to this folder as well.

#. This is the "Filemount" placeholder record defining
   "fileadmin/webfolder/" as a filemount and is mounted because this
   filemount has been specifically added to the users record. (See the
   section above about relative filemounts)

(The two yellow folders named "test" are some that have been created
as a test from the backend.)

If we log in as the user "guest" (uid=2) we should also see some
mounted directories:

|img-54|

#. This is the user "guest"s  *private* home directory in
   "/my\_absolute\_path/users/2/". Only the user "guest" has access to
   this directory.

#. This is the "public" home directory that belongs to the group
   "guest\_group" (uid=1). This is mounted because the "guest" user has
   been assigned membership of the "guest\_group"! Since the user named
   "admin" has access to this directory as well, they can share files
   here!

#. The user "guest" has the Filemount "My Abs Path" assigned to him which
   leads to that path being mounted of course (see section on absolute
   filemounts above).

#. The user "guest" has the Filemount "My Relative Path" assigned to him
   which mean it is mounted also!


Webspace/FTPspace
"""""""""""""""""

TYPO3 detects if mounted paths are reaching into the domain of the
PATH\_site constant. If that is the case the folder is recognized as
being in the "Web-space" (yellow folder icon). If a folder is  *not*
within PATH\_site it is assumed to be a folder internally on the
server and thus in "FTP-space" (blue folder icon).

|img-55|

The significance of this is what kinds of files are allowed the in the
one and in the other "space". This is determined by the variable
$TYPO3\_CONF\_VARS['BE']['fileExtensions']::

               'webspace' => array('allow'=>'', 'deny'=>'php3,php'),
               'ftpspace' => array('allow'=>'*', 'deny'=>'')

This configuration is the default rule on file extensions allowed
within each space. Basically it says that in FTP-space all files are
allowed, but in Web-space "php3" and "php" is disallowed!

Having restrictions like this also means that unzipping of files and
moving whole directories from FTP- to Web-space is not possible within
the backend of TYPO3. This can be expressed as these rules:

- In web-space you cannot unzip files

- You cannot copy or move folders from ftp- to web-space.

(see the classes basicfilefunctions, extfilefunctions and
tce\_file.php plus the document "TYPO3 Core API")

**Notice:** In addition to the rules set up in
$TYPO3\_CONF\_VARS['BE']['fileExtensions'] there is a global regex
pattern which will also disqualify ANY file matching from being
operated upon. That is set in
$TYPO3\_CONF\_VARS['BE']['fileDenyPattern'].

For details about the configuration of these options please read the
source comments in "t3lib/config\_default.php".


Filemounts on windows servers
"""""""""""""""""""""""""""""

Currently not know if it works and what limitations it might have.
Probably they have to be on the same harddisk as the main site.

