.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Info module
^^^^^^^^^^^

The Web > Info module as provided by the core is an empty shell. It
provides an API that extensions can use to attach function menu items
to the Info module.

In the screenshot below you can see three options in the Function Menu
which are coming from installed extensions:

|img-141|

The idea of the Web > Info module is to be a host module for backend
applications that wish to present information /analysis of pages or
branches of the page tree. This could be website statistics, caching
status information etc. In the case above it is a view of available
record types in the branches in the tree.

Conceptually the Web > Info module is different from the `Web > Functions
<#Functions%20module%7Coutline>`_ module only by  *primarily showing
information* rather than offering functionality. It is up to extension
programmers to decide in which of these two modules they want to
insert functionality.

