.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Additional security measures you can take:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Add a .htaccess file to the typo3/ source code directory. This will
  “webserver protect” the backend interface. Backend users will have to
  type in two passwords: First the general webserver password, then the
  user-specific TYPO3 password.The authenticated web-server user is not
  used by TYPO3 in any way. It just adds another gate in the
  authorization process. **Notice:** This solution will not work if you
  are using file resources (such as images) from extensions in your
  frontend! That might be the case if your site uses frontend plugins
  from extensions installed as "system" or "global". If an image is
  referenced on the site it will trigger an authorization box to pop up!
  The solution could be to install the extension as "local" (in
  typo3conf/ext/) where the directory is not password protected.

- Add IP-filtering (see TYPO3\_CONF\_VARS[BE][IPmaskList]) - this
  enables you to lock out any backend users which are not coming from a
  certain IP number range.

- Add lockToDomain in be\_users/be\_groups records (makes sure that
  users are logging in only from certain URL's - maybe some secret
  admin-url you make?)

- `Change name of the "typo3/" backend directory <#Changing%20the%20defa
  ult%20%E2%80%9Ctypo3/%E2%80%9D%20directory%7Coutline>`_ (makes it
  harder to guess the administration URL).

- Set the TYPO3\_CONF\_VARS[BE][warning\_mode] and
  TYPO3\_CONF\_VARS[BE][warning\_email\_addr] - that will inform you of
  logins and failed attempts in general.

- Use https for all backend activity. That will make sure that your
  passwords and data communication with the server are truely encrypted.
  TYPO3\_CONF\_VARS[BE][lockSSL]=1 will force users to use https.

