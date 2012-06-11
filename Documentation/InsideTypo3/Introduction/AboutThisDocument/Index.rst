.. include:: Images.txt

.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. ==================================================
.. DEFINE SOME TEXTROLES
.. --------------------------------------------------
.. role::   underline
.. role::   typoscript(code)
.. role::   ts(typoscript)
   :class:  typoscript
.. role::   php(code)


About this document
^^^^^^^^^^^^^^^^^^^

For most people TYPO3 is equivalent to a CMS providing a backend for
management of the content and a frontend engine for website display.
However TYPO3s core is natively designed to be a general purpose
framework for management of database content. The core of TYPO3
delivers a set of principles for storage of this content, user access
management, editing of the content, uploading and managing files etc.
Many of these principles are expressed as an API (Application
Programmers Interface) for use in the  *extensions* which ultimately
adds most of the real functionality.

|img-3|

So the  *core* is the skeleton and  *extensions* are the muscles,
fibers and skin making a full bodied CMS. In this document I cut to
the bone and provide a detailed look at the core of TYPO3 including
the API available to the outside. This is supposed to be the final
technical reference apart from source code itself which is - of course
- the ultimate documentation.


Intended audience
"""""""""""""""""

This document is intended to be a reference for experienced TYPO3
developers. For intermediates it will help you to become experienced!
But the document presumes that you are well familiar with TYPO3 and
the concepts herein. Further it will presume knowledge in the
technical end; PHP, MySQL, Unix etc.

The goal is to take you "under the hood" of TYPO3. To make the
principles and opportunities clear and less mysterious. To educate you
to help continue the development of TYPO3 along the already
established lines so we will have a consistent CMS application in a
future as well.And hopefully my teaching on the deep technical level
will enable you to educate others higher up in the "hierarchy". Please
consider that as well!


Up-to-date information?
"""""""""""""""""""""""

We are committed to keeping this document up-to-date. We also want
this document and related documents to contain enough information for
you to develop with TYPO3 effectively. But guess what - in any case
the source  *is* updated before  *this* document is and therefore the
*ultimate* source of both up-to-dateinformation and  *more*
information is peeking into the source scripts! And for the source
scripts we are also trying to keep them well documented.

So generally the source code is the final authority, the final place
to look for features and get a precise picture of function arguments
etc. The documentation inside the source scripts will be short and
precise, no examples, not much explanation. But enough for people
knowing what to look for. This document - an other documents like "
`TYPO3 Core API <../Sites/typo3/doc_core_api/doc/manual.sxw>`_ " -
should provide the greater picture explanations for use.

If you find that sections in this document are missing something,
please help the author by notifying him and possibly supply a piece of
text which could serve as the supplement you want to have added. You
can also use the annotation feature in the online version at
TYPO3.org.

**Notice:** TYPO3 version 4 bears a new visual interface (skin) that
is not reflected in the screenshots of this document. However, this
does not have any impact on the content itself.

