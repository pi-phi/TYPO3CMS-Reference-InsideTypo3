

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


XSS (Cross Site Scripting)
^^^^^^^^^^^^^^^^^^^^^^^^^^

TYPO3 has  *not* been thoroughly screened for XSS bugs. However the
general coding style of TYPO3 has always implemented
htmlspecialchars() and strip\_tags() where necessary so the state in
regard to XSS should be fairly sound. We also include guidelines for
preventing XSS bugs in the official Coding Guidelines.

If you have found XSS bugs or generally want to help out by testing or
offering expertise on the matter, please let us know.

