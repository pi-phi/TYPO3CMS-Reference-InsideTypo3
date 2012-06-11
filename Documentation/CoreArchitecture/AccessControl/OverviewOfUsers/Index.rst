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


Overview of users
^^^^^^^^^^^^^^^^^

Since TYPO3 offers such a comprehensive scheme for controlling
permissions it quickly becomes a problem to verify that all
permissions are set correctly. To help alleviate this problem the
extension "beuser" is worth mentioning.

This extension installs a backend module in "Tools > User Admin"
("admin" only access). Here you can compare the settings for users
based on all permission types. For example the backend users are
grouped by membership of backend groups in this example:

|img-74|

As you can see the users "admin" and "guest" shares membership of
"guest\_group" while the user "newuser" is member of "New group".

Criterias can also be combined:

|img-75|

Viewing the TSconfig structure for users is also very handy:

|img-76|

Notice how the default TSconfig for "admin" users clearly is set.
Likewise for the "options.shortcutFrame" setting we applied for the
"guest" user earlier while the newuser has no TSconfig.

Now, lets add the shortcutFrame for the "newuser" as well:

|img-77|

As you can see, even if we configure the TSconfig of the user
"newuser" little differently (adding a comment, using braces) the
actually configured values for the "guest" and "newuser" users is the
*same* now - which qualifies them to be grouped together when grouping
by TSconfig.


Switch user
"""""""""""

Apart from edit, disabled and delete buttons located in the "User
Admin" module you can also switch user easily by a single click if the
[SU] button:

|img-78|

You cannot switch back for security reasons, so you will have to
logout and login as "admin" again. However this feature is extremely
practical if you need to login as another user since you don't have to
expose/change their passwords!

**Tip:** Running MSIE (at least) you can start MSIE twice from the
Program Menu and each instance will have a different process and
"cookie-scope"; The point is that you can login as "admin" in the one
MSIE browser window and as another user in the other window - in the
same database! This is possible because the two MSIE instances "don't
know" about each other.


Previewing user settings
""""""""""""""""""""""""

However you don't have to switch user to just check how that user
would see the backend. You can simply click the username and you will
have a nice view like this:

|img-79|

This basically lists all information you could dream of for that user.
In particular the calculated permissions for "This user" (1) is nice
since that is the sum of the user/group/everybody permissions as they
will apply to this user for each page in his DB mounts.

**"Non-mounted readable pages"** (2) could potentially be a security
problem. Those pages are not mounted as DB mounts and thus not
visible/clickable in the page tree. But guessing an id of one of those
pages and sending that id to the Web>List module would list records on
these pages. Most likely you don't want that. Further the danger is
even more serious if you have Frontend Edit enabled in the CMS
frontend. However  *there is no problem* unless you change a default
setting; As long as TYPO3\_CONF\_VARS['BE']['lockBeUserToDBmounts'] is
true (which it is by default) pages will be accessible  *only* if the
they appear  *within* the DB mounts - that makes security management a
whole lot easier since you  *don't* have to worry about "Non-mounted
readable pages" at all.

