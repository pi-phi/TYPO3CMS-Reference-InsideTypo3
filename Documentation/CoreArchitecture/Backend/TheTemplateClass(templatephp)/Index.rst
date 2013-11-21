.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


The template class (template.php)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most backend scripts include another core script than "init.php". That
is "template.php". ::

   require ('init.php');
   require ('template.php');

"template.php" contains a class "template". This class is used to
output HTML-header, footer and page content in the backend.

template.php does this:

- Initially an obsolete function, fw($str), is defined. This just
  returns the input string un-altered. May be removed in the future as
  it's obsolete and here for backwards compatibility only. If you use
  this function in your modules, then stop doing that!

- Defines the class "template" which contains the HTML output related
  methods for creating backend documents.

- Defines four extension classes of the template class: bigDoc, noDoc,
  smallDoc, mediumDoc. Each of them presets a certain width of the
  outputted page by specifying a class for a wrapping DIV-tag.

- Includes sysext/lang/lang.php which contains the class "language" for
  management of localized labels in the backend. It also contains an
  instance of the character set conversion class, "t3lib\_cs".

- Creates the global variables $TBE\_TEMPLATE and $GLOBALS['LANG'] as instances of
  the classes "template" and "language" respectively.

"template.php" requires init.php to have been included on beforehand.

This is the variables and classes available in addition after
inclusion of "template.php":


Variables
"""""""""

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Global variable
         Global variable

   Defined in
         Defined in

   Description
         Description

   Avail. in FE
         Avail. in FE


.. container:: table-row

   Global variable
         $TBE\_TEMPLATE

   Defined in
         template.php

   Description
         Global backend template object for HTML-output in backend modules

   Avail. in FE


.. container:: table-row

   Global variable
         $GLOBALS['LANG']

   Defined in
         template.php

   Description
         Localization object which returns the correct localized labels for
         various parts in the backend.

         It also contains an instance of the "t3lib\_cs" class in
         $GLOBALS['LANG']->csConvObj

   Avail. in FE


.. container:: table-row

   Global variable
         *$LOCAL\_LANG*

   Defined in
         Optionally included "locallang" file.

   Description
         Stores language specific labels and messages. Requires a "local\_lang"
         file to have been included in the global space.

         **Notice:** This variable is unset in "config\_default .php" for your
         convenience. So don't set the $LOCAL\_LANG array prior to "init.php".

   Avail. in FE
         -


.. container:: table-row

   Global variable
         *$TCA\_DESCR*

   Defined in
         [on-the-fly]

   Description
         Could be set to contain help descriptions for fields and modules. Is
         set by API function in the "language" class.

         Unset in "config\_default.php"

   Avail. in FE


.. ###### END~OF~TABLE ######


Classes
"""""""

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Class
         Class

   Included in
         Included in

   Description
         Description

   Avail. in FE
         Avail. in FE


.. container:: table-row

   Class
         template

   Included in
         [optionally included after init.php, see next section]

   Description
         Global backend template class for HTML-output in backend modules,
         instantiated inside template.php as $TBE\_TEMPLATE

   Avail. in FE
         -


.. container:: table-row

   Class
         language

   Included in
         template.php

   Description
         Localization class which returns the correct localized labels for
         various parts in the backend. Instantiated as $GLOBALS['LANG']

   Avail. in FE
         -


.. ###### END~OF~TABLE ######


Example: A dummy backend script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As an good example of how backend scripts (modules) should be
constructed, please look at the dummy.php file::

   /**
    * Dummy document - displays nothing but background color.
    *
    * @author    Kasper Skårhøj <kasper@typo3.com>
    * Revised for TYPO3 3.6 2/2003 by Kasper Skårhøj
    * XHTML compliant content
    */

   require ('init.php');
   require ('template.php');

   // ***************************
   // Script Classes
   // ***************************
   class SC_dummy {
       var $content;

       /**
        * Create content
        */
       function main()    {
           global $TBE_TEMPLATE;

               // Start page
           $TBE_TEMPLATE->docType = 'xhtml_trans';
           $this->content.=$TBE_TEMPLATE->startPage('Dummy document');

               // End page:
           $this->content.=$TBE_TEMPLATE->endPage();
       }

       /**
        * Print output
        */
       function printContent()    {
           echo $this->content;
       }
   }

   // Include extension?
   if (defined('TYPO3_MODE') && $TYPO3_CONF_VARS[TYPO3_MODE]['XCLASS']['typo3/dummy.php'])    {
       include_once($TYPO3_CONF_VARS[TYPO3_MODE]['XCLASS']['typo3/dummy.php']);
   }




   // Make instance:
   $SOBE = t3lib_div::makeInstance('SC_dummy');
   $SOBE->main();
   $SOBE->printContent();


(In addition a script must include opening and closing tags for php
(<?php ... ?>) and a copyright header defining the author and GNU/GPL
license. See almost any script in the backend for an example)

In this example you see the following important elements:

- init.php is included by require(): We can now know that a backend user
  is authenticated, that there is a database connection etc.

- template.php is included by require(): We can now create backend HTML-
  output and localized labels.

- Script class is defined (here: "SC\_dummy", typically named "SC\_" +
  script name). All processing should take place inside this class

- Possible inclusion of an extension class for the "SC\_dummy" (this is
  what happens in the lines after "// Include extension?"

- Finally the script class is instantiated and the relevant functions
  are called - here main() and printContent(). Which functions needs to
  be called from the global space depends on what  *you* have put into
  your class!

Inside the script class these basic steps for HTML output is taken:

- The method $TBE\_TEMPLATE->startPage('Dummy document') is called: This
  returns the header section of the output HTML page with the page title
  set to "Dummy document". Prior to this function call the docType is
  set to XHTML Transitional (optional). You can also specify other
  optional values like additional CSS styles, JavaScript etc.

- The method $TBE\_TEMPLATE->endPage() is called: This returns the page
  footer.

- In between the two function calls you can basically output any HTML
  you like as the page content. <body> tags have been set and typically
  the whole page is wrapped in a DIV tag as well.

The HTML output of dummy.php will look like this::

   <?xml version="1.0" encoding="iso-8859-1"?>
   <?xml-stylesheet href="#internalStyle" type="text/css"?>
   <!DOCTYPE html
        PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
   <html>
   <head>
     <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"/>
     <meta name="GENERATOR" content="TYPO3 3.6.0-dev, http://typo3.com, &#169; Kasper Sk&#197;rh&#248;j 1998-2003, extensions are copyright of their respective owners." />
     <title>Dummy document</title>

             <link rel="stylesheet" type="text/css" href="stylesheet.css"/>

             <style type="text/css" id="internalStyle">
                     /*<![CDATA[*/
                             A:hover {color: #254D7B}
                             H2 {background-color: #9BA1A8;}
                             H3 {background-color: #E7DBA8;}
                             BODY {background-color: #F7F3EF;}

                     /*]]>*/
             </style>


   </head>
   <body>

   <!-- Wrapping DIV-section for whole page BEGIN -->
   <div class="typo3-def">


   ... [additional content between startPage() and endPage() will be inserted here!] ...


     <script type="text/javascript">
               /*<![CDATA[*/
             if (top.busy && top.busy.loginRefreshed) {
                     top.busy.loginRefreshed();
             }
              /*]]>*/
     </script>

   <!-- Wrapping DIV-section for whole page END -->
   </div>
   </body>
   </html>

The maroon coloured content is created by startPage()

The teal coloured content is created by endPage()

The green/bold line represents the position where your custom output
will be placed in the document.


API documentation
"""""""""""""""""

There is a host of methods inside the template class which can be
used. Some of these are documented in "TYPO3 Core API" and others by
examples in various Extension Programming Tutorials.

