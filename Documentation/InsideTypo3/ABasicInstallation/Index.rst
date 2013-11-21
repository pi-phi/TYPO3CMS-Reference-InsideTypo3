.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


A basic installation
--------------------

Since we are dealing with the core of TYPO3 it might help us to make a
totally trimmed down installation of TYPO3 with  *only* the core -
then we can see what is actually left...

First of all the general introduction to the source code file
structure is found in the " :ref:`Installation and Upgrade Guide
<t3install:start>` ". So I'll not be going into details on that here.

For the coming sections in this document I have made a directory
"coreinstall" on the same level as an installation of the source code.
The "coreinstall" directory is going to be the base directory of the
installation (this path is internally in TYPO3 known as the constant
"PATH\_site"). This is where the website would run from normally. ::

   [root@T3dev 32]# ls -la
   total 27768
   drwxr-xr-x   21 httpd    httpd        4096 Feb 14 14:25 ./
   drwxr-xr-x    4 httpd    httpd        4096 Jan 16 19:59 ../
   drwxr-xr-x    2 httpd    httpd        4096 Feb 14 14:25 coreinstall/
   lrwxrwxrwx    1 httpd    httpd          20 Feb 14 12:05 typo3_src -> typo3_src-3.6.0-dev/
   drwxr-xr-x    6 httpd    httpd        4096 Jan 30 17:23 typo3_src-3.6.0-dev/


.. toctree::
   :maxdepth: 5
   :titlesonly:
   :glob:

   TheBackendAdminstrationDirectoryTypo3/Index
   Typo3confLocalconfphp/Index
   TheInstallTool/Index
   BasicCoreInstallationSummary/Index

