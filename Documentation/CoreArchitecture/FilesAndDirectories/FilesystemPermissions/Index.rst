

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


Filesystem permissions
^^^^^^^^^^^^^^^^^^^^^^


How does the UNIX-filesystem permissions interact with TYPO3?
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

The answer is simple: TYPO3 runs as the user, PHP "runs" as. This
could depend on the httpd.conf file of Apache. Default is "nobody" as
far as I know. On Debian installations it is "www-data".

The main thing is, that TYPO3 must be able to write to certain folders
in order for the file-administration to work. This means that after
installation of TYPO3, you should alter the user of the scripts and
folders, probably with the "chown" command.

If you have access to the webserver through FTP, you might be
uploading scripts with yourself as user. These scripts might be
executable by Apache as PHP-scripts but when the scripts need to write
to eg. the upload-folder, this folder might be owned by "you" and
thereby TYPO3 does not work. Therefore; the folders TYPO3 need write-
access to must be writeable by the Apache-user.

Folders that requires write access are fileadmin/\* and uploads/\* for
the frontend and typo3temp/ for both frontend and backend. Furthermore
for extensions directories typo3/ext/ and typo3conf/ and sub
directories must be writeable for PHP as well.

Another issue is if you mount user-directories (see the localconf-
file). You may mount a directory to which you have ftp-access. But if
you do so, files uploaded to this directory may not be deleted by
TYPO3. That's normally not a problem - you can delete them again by
ftp, but it's much worse if you do not enable read-access for the
Apache-user to that directory. Then the directory-structure will not
be read and it does not show up on the file-tab.

Experience suggests that if you run in a two-user mode (one use for
FTP, another for PHP-script execution) you should do this to make
TYPO3 work seemlessly:

- Make each user a member of the other users group

- Set "775" permissions on files and folders that should be writeable by
  both

- Set "[user1].[user2]" owner/group on files and folders

