

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


Default security includes:
^^^^^^^^^^^^^^^^^^^^^^^^^^

The security dealt with here regards the backend of TYPO3.

- Passwords for backend login are not sent clear-text (front-end user
  logins are!). They are md5-hashed together with a unique string sent
  from the server and thus hard to decipher. Editing the passwords in
  the backend interface also md5-hashes the password before it's sent to
  the server.This is not true encryption, it just makes it hard to
  find/guess the passwords.

- Sessions for backend and frontend users are done with a 32 byte cookie
  (md5-hash) which is looked up in the database and restores the
  session. A session lasts for little less than 2 hours with idle-time.
  Sessions might be locked to (parts of) the remote IP address of the
  user and the HTTP\_USER\_AGENT identification string to prevent
  session hi-jacking.

