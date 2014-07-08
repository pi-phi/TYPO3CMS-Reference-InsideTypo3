.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


The locallang files for CSH
^^^^^^^^^^^^^^^^^^^^^^^^^^^

First of all you are strongly encouraged to use the locallang file
structure where the default document sets "EXT" as value for the
localized labels so that sub-files are included. This will load the
system less and make it all easier to manage.

Then there are a few other rules to follow:

- Prefix the locallang files "locallang\_csh\_" so that translators can
  easily spot these files (which has a secondary priority compared with
  other locallang files!).

- Observe the filename length, which should be maximum 31 chars in
  total! Since the prefix "locallang\_csh\_" takes 14 chars, the
  extension ".xml" takes four and any "subfile-suffix" (fx. "dk.") would
  take three, there is 31-14-4-3 = 10 chars left. So lets say you have 9
  characters to name the file to be safe.

  Examples where "pages" (5 chars) is the unique name::

     locallang_csh_pages.xml    =>   23 chars
     dk.locallang_csh_pages.xml      =>   26 chars

- Observe the label-key naming by the syntax [fieldname].[type-
  key].[special option] (see previous section)

- Label-key names that are prefixed "\_" can safely be used - the prefix
  is simply removed! This is encouraged for the "seeAlso" and "image"
  field names since those are in common for all languages and therefore
  doesn't need translation (the typo3.org translation tool ignores
  label-keys which are prefixed "\_").

- When used with database tables: Blank fieldnames are used for
  information about the database table itself - non-blank fieldnames are
  expected to point to the actual fieldnames.

- You can place images in a subfolder, "cshimages/", to where the
  locallang-file is located and they will be shown in a selector box
  inside the translation tool.


Syntax for the type-keys content
""""""""""""""""""""""""""""""""

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   type-key
         type-key

   Syntax
         Syntax


.. container:: table-row

   type-key
         description

   Syntax
         Text / XHTML. Mandatory.


.. container:: table-row

   type-key
         details

   Syntax
         Text / XHTML. Optional.


.. container:: table-row

   type-key
         syntax

   Syntax
         Text / XHTML. Optional.


.. container:: table-row

   type-key
         image\_descr

   Syntax
         Text. Optional.


.. container:: table-row

   type-key
         image

   Syntax
         Reference to an image (gif,png,jpg) which will be shown below the
         syntax field (before seeAlso)

         The reference must be

         - a) either relative to the TYPO3\_mainDir (fx. "gfx/i/pages.gif") or

         - b) related to an extension (fx.
           "EXT:context\_help/descr\_imgs/hidden\_page.gif")

         You can supply a comma list of image references in order to show more
         than one image. The image\_descr value will be split per linebreak
         and shown under each image.


.. container:: table-row

   type-key
         seeAlso

   Syntax
         Internal hyperlink system for related elements. References to other
         TCA\_DESCR elements or URLs.

         **Syntax:**

         - Separate references by comma (,) or line breaks.

         - A reference can be:

           - either a URL (identified by the 'second part' being prefixed "http",
             see below)

           - or a [table]:[field] pair

         - If the reference is an external URL, then the reference is splitted by
           vertical line (\|) and the first part is the link label, while the
           second part is the "http"-URL

         - If the reference is to another internal TCA\_DESCR element, then the
           reference is splitted by colon (:) and the first part is the  *table*
           while the second is the  *field* .

         External URLs will open in a blank window. The links will be in
         italics.

         Internal references will open in the same window

         For internal references the permission for table/field read access
         will be checked and if it fails, the reference will not be shown.

         **Example:**

         pages:starttime , pages:endtime , tt\_content:header , Link to
         TYPO3.org \| http://typo3.org/


.. container:: table-row

   type-key
         alttitle

   Syntax
         Alternative title shown in CSH pop-up window.

         For database tables and fields the title from TCA is fetched by
         default, however overridden by this value if it is not blank.

         For modules (tablename prefixed "\_MOD\_") you must specify this
         value, otherwise you will see the bare key being output.


.. ###### END~OF~TABLE ######

In all cases of "Text" above <strong>, <em>, <b>, and <i> is allowed
as HTML tags.  *Make HTML-tag names and attributes in lowercase! Must
be XHTML compliant.*

