.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


((generated))
^^^^^^^^^^^^^

Backend main- and sub-modules
"""""""""""""""""""""""""""""

The backend menu reflects the hierarchy of  *modules* in TYPO3,
divided into  *Main modules* and  *Sub modules* . This was discussed
in the `introduction to the backend interface
<#Backend%20interface%7Coutline>`_ . Their properties are:

- **Backend Menu** They appear in the backend menu and "About modules"
  screen. They have an icon, title, description etc.

- **Access control** They can be access controlled for backend users and
  groups automatically (depends on configuration).

|img-80|

There is a special kind of module;  **Frameset modules** are main
modules in TYPO3 which provides a navigation/list frameset for sub-
modules. The "Web" and "File" main modules are frameset modules.


"Function Menu" module
""""""""""""""""""""""

The "Function Menu" is the selector box menu you will often find in
the upper right corner of backend modules. By that selector you can
select sub-functionality within that module. Often this functionality
is hardcoded into the backend module. In other cases (like the core
modules `Web>Info <#Info%20module%7Coutline>`_ and `Web>Functions
<#Functions%20module%7Coutline>`_ ) there is an API which allows you
to add additional items to the function menu and specify which PHP-
class to call for rendering the content of that item.

|img-81|

The idea of Function Menu modules is that you can add minor
functionalities without introducing a whole new backend module which
shows up in the menu. Their properties are:

- **Discrete** Adds functionality discretely or in certain contexts
  (like in the Web>Template module you would add functionality related
  to TypoScript Templates).

- **Simple** Inherits access control and default configuration from main
  module.


Stand-alone backend scripts
"""""""""""""""""""""""""""

Finally, a script can also work in the backend without being a "real"
module (like those in the menu) or Function Menu module. Such a script
basically needs to include the "init.php" file from the TYPO3 main
folder in order to authenticate the backend users and include the
standard classes of TYPO3. Technically this is done by using a subset
of the module API. Such a stand alone script is what you will normally
get if you create a new CSM item that has to link to a backend enabled
script.

|img-82|

