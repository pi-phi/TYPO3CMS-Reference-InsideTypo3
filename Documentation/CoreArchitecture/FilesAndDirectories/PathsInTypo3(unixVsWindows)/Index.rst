.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Paths in TYPO3 (UNIX vs. Windows):
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Absolute paths are necessary in the backend in order to support
symlinking of the backend code (UNIX).

All paths are using single forward slashes (mydir/myfile.php - right!)
opposed to backslashes (mydir\\myfile.php - WRONG!).

All absolute paths should begin with either "/" or "x:/", eg.
"/mydir/myfile.php" (unix) or "C:/mydir/myfile.php" (windows). Please
use the function t3lib\_div::isAbsPath($path) to check absolute paths.
This function will return true if absolute. There are also a few other
API functions which are very recommended for security reasons:
t3lib\_div::getFileAbsFileName() will return the absolute filename for
you from a relative path and further check that the path in the input
is valid. t3lib\_div::validPathStr() is also nice since it checks for
"..", "//" and "\\" in the path.

See "TYPO3 Core API" for more details on `high priority API functions
<#High%20priority%20functions%20(CGL%20requirements)%7Coutline>`_ .

