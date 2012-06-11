

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


Notice!
^^^^^^^

Generally, backend users in TYPO3 are expected to be trusted to a
certain degree. At least TYPO3 assumes that you are in control of your
backend users to a large extend and have a good grip on their
intentions. Therefore you should be aware that:

- Backend users are typically allowed to create HTML content elements
  which inserts  *pure* HTML on webpages! Other elements allow for the
  same and there are many places where URLs are possible to insert. All
  of this means one thing: Ordinary backend users maintaining content
  *can exploit XSS techniques* since they can insert content on pages!
  This is  *not* a bug in TYPO3 but a “feature” which is impossible to
  avoid if you at the same time want people to do exactly that; insert
  pure HTML on pages!Of course the problem is not big; you can always
  track down which user might have inserted malicious code on the pages
  through the backend log!

