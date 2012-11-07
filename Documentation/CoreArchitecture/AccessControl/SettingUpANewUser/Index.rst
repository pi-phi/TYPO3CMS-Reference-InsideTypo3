.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Setting up a new user
^^^^^^^^^^^^^^^^^^^^^

This is a very quick tutorial on setting up a Backend User. It only
outlines the steps you will typically have to take and it doesn't
pretend to explain a lot of alternatives etc. To properly configure
user schemes you must have a detailed understanding of how access
control is done in TYPO3. That is what you should have gained from
reading the previous pages about access control. But if you need
general guidelines, typical setup suggestions etc, you will have to
find a tutorial on the subject.


1: Create a new Backend User record
"""""""""""""""""""""""""""""""""""

|img-56|


2: Enter unique username, password, name, email and language
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

|img-57|

*Logging in now, this is what the user will see:*

|img-58|


3: Create a group, setup access lists, assign membership of group
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Click the "Create new" icon:

|img-59|

... enable the access lists, and add the relevant entries:

|img-60|

Edit the user record again and set the membership of the group:

|img-61|

|img-62|

*Logging in now, this is what the user will see:*

|img-63|


4: Set up DB mount point
""""""""""""""""""""""""

Either do this for the group you created or for the user record
itself. If you chose to set up the DB mount for the group you will be
able to share the DB mount for all members of that group that has the
"Mount from groups:" / "DB Mounts" flag set.

|img-64|

Then make sure to set the permissions recursively for that page so
either the user owns the page and subsequent pages or that the user is
member of the group owning the pages (or of course allowing
"everybody" access).

|img-65|

Then select the permissions you want to assign. In this example the
user will be the new owner and his member group will be the group of
the pages three levels down. Other configurations can work as well of
course. Most importantly for the DB mount is that the "Show page"
permission is set for the DB mount page. Otherwise the mount will not
even be shown!

|img-66|

Result:

|img-67|

*Logging in now, this is what the user will see in the Web > List
module:*

|img-68|


5: Set up a File mount (optional)
"""""""""""""""""""""""""""""""""

Optionally you can create a file mount for the user. It's not a
requirement since users can upload files directly in editing forms,
but it might be more flexible for your users if they can create a
online archive of files for reuse.

Most typically a user has access to a subfolder in "fileadmin/". This
can be achieved like this:

**Create the Filemount record:**

|img-69|

**Create the folder "fileadmin/user\_uploads/":**

Since you as an "admin" user has access to "fileadmin/" by default,
you can do this easily through the backend:

|img-70|

**Add the file mount record to the File mounts of the group "New
group":**

|img-71|

**Make sure the flag "Mount from groups:" / "File Mounts" is set:**

|img-72|

*Logging in now, this is what the user will see in the File > List
module:*

|img-73|

