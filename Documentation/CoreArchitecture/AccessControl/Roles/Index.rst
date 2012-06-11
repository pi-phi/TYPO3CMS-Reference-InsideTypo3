

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


Roles
^^^^^

Another approach to setting up users is very popular - roles. This
concept is basically about identifying certain roles that users can
take and then allow for a very easy application of these roles to
users.

TYPO3s access control is far more flexible and allows for so detailed
configuration that it lies very far from the simple and straight
forward concept of roles. This is necessary as the foundation if a
system like TYPO3 should fit many possible usages.

However "roles" are possible to  *create* ! You simply have to see
user-groups as representing roles! So what you do is to:

#. Identify the roles you need; Developer, Administrator, Editor, Super
   User, User, ... etc.

#. Configure a group for each role. This group so configure the access
   permissions for each role.

#. Consider having a general group which all other groups includes - this
   would basically configure a shared set of permissions for all users.

So "roles" are simply user groups defined to work as roles. However we
might still spend some efforts to make some public recommendations for
roles as a guideline for people (since the configuration of these
roles will otherwise be a lot of work) and further the native access
control options in the TYPO3 core might need some extending in order
to accommodate all needed role configurations.

