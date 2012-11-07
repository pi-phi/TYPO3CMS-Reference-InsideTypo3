.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Recommendations
^^^^^^^^^^^^^^^

In the core group we are only directly concerned with security of the
source code libraries/scripts plus extensions. Whatever scripts are
located in fileadmin/ or typo3conf/ - basically all local,  *site-
specific* scripts - are outside of our domain. However these are our
recommendations on how to deal with all the site specific issues. Some
of these suggestions are for paranoid users, but now we mention them
and you can determine the threat yourself.

- Make sure your PHP-scripts does not output the path on the server if
  they are called directly. If you use the testsite package there are
  example scripts in fileadmin/ directory which will do so. That is
  called "path disclosure" and poses a security threat (some argues).

- **SQL-dumps:** Don't store SQL-dumps of the database in the webroot -
  that provides direct access to all database content if the file
  position is known or guessed.

- **locallang.php:** You might move the typo3conf/locallang.php file to
  a position outside of webroot and then use the typo3conf/localconf.php
  file to just include this other file from the absolute position. Some
  argues that it's a security problem to have the configuration file
  located inside the webroot. **Example:** Make a file
  "/home/mydir/real\_localconf.php" and put your configuration into that
  file. Then make the real "typo3conf/localconf.php" look like this::

     <?php
     require("/home/mydir/real_localconf.php");
     ?>

- **typo3/dev/ folder:** You might remove the typo3/dev/ folder since it
  contains development scripts only. They are however by default (or
  should be!) disabled by die() function calls.

- **Install Tool:** Make sure to protect the Install Tool since it can
  be extremely harmful. By default the typo3/install/index.php script
  should be blocked by a die() function call which can be commented out
  when you need the script. Furthermore, calling the die() function
  depending on the IP address from REMOTE\_ADDR is not considered secure
  enough! You should also change the default password from "joh316" to
  something else. Further you could add a ".htaccess" file to the
  "typo3/install/" directory. If you are really paranoid you can totally
  remove the typo3/install/ directory, but that's probably too far to
  go.

- **Disable "Directory listing"** in the webserver or alternatively add
  blank "index.html" to subdirectories like uploads/\*, typo3conf/\* or
  fileadmin/\*. Most likely you don't want people to browse freely in
  your subdirectories to TYPO3.

(Thanks to Martin Eiszner / @2002WebSec.org for pointing out some of
these issues)

