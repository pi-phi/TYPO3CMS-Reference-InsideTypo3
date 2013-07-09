.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


PHP settings
^^^^^^^^^^^^

PHP settings can also greatly influence security. If you read the
header of a "php.ini" file you will normally find a list of the latest
list of recommended settings for a production environment. Our coding
guidelines are encouraging developers to program code compliant with
these guidelines.

As a little snapshot these settings affects security and could be
enabled:

- Settings that will prevent PHP from revealing information about your
  system if an error occurs. However, this will be very disturbing to
  turn on in a development environment::

     log_errors = On
     display_errors = Off

- Enabled "open\_basedir" and "safe\_mode" for your server (TYPO3 3.6.0
  is compliant!)

