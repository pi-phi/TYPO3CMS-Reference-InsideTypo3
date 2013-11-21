.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Functions module
^^^^^^^^^^^^^^^^

The Web > Functions module as provided by the core is an empty shell. It
provides an API that extensions can use to attach function menu items
to the Web > Function module.

In the screenshot below you can see the "Wizard" option in the
Function Menu which is coming from an installed extension:

|img-143|

The idea of the Web > Functions module is to be a host module for
backend applications that wish to perform processing of pages or
branches of the page tree. In the case above it is a wizard
application for batch creation of pages in the page tree.

Conceptually the Web > Functions module is different from the `Web > Info
<#Info%20module%7Coutline>`_ module only by offering  *processing
functionality* rather than offering information only. It is up to
extension programmers to decide in which of these two modules they
want to insert functionality.

