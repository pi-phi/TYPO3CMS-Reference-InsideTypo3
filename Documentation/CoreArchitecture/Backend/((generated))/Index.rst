.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


((generated))
^^^^^^^^^^^^^

Backend interface
"""""""""""""""""

The backend interface is (typically) found in the typo3/ directory
(constant TYPO3\_mainDir).

Visually it is divided by a frameset into these sections:

|img-14|

#. alt\_main.php: This script is redirected to after login from
   index.php. It will generate the frameset and include a minor set of
   JavaScript functions and variables which will be used by the other
   backend scripts with reference to the "top" JavaScript object. (JS
   reference: "top")

#. alt\_toplogo.php: Simply creates the logo in the upper left corner of
   the backend. (JS reference: "top.toplogo")

#. alt\_topmenu\_dummy.php: By default it displays nothing. But when
   users click an icon of a file or database record and a context
   sensitive menu is displayed, then it is loaded into this frame. Then -
   depending on the capabilities of the client browser - the menu is
   either shown in this frame or the frame will remain blank and just
   write the menu content back to the calling frame where a DIV-layer
   will be created with the menu content dynamically. Depending on user
   configuration (User > Setup: Select navigation mode = "Icons in top
   frame") you might also see a list of menu icons in this bar as the
   default document (see below). (JS reference: "top.topmenuFrame")

#. alt\_menu.php: Displays the vertical menu of backend modules. (JS
   reference: "top.menu")

#. alt\_intro.php: By default the "About modules" content is shown here.
   However users might be shown the task center right away if they set
   that option in the User > Setup screen (if the "taskcenter" extension
   is installed). Otherwise this frame will contain module scripts
   depending on selections in the menu of course. One special instance of
   this is "Frameset modules" like the Web and File main modules since
   they will display a frameset with a page/directory tree and a
   record/file list (see below). (JS reference: "top.content")

#. alt\_shortcut.php: This frame is  *optionally* displayed depending on
   user configuration. For "admin" users it's always shown. For other
   users it must be specifically enabled (User TSconfig:
   "options.shortcutFrame"). (JS reference: "top.shortcutFrame")

Finally the backend can be configured for "condensed mode" and there
are also a few alternative options for how the menu is displayed.


Alternative menu: Selectorbox
"""""""""""""""""""""""""""""

One of those alternative options include having a selector box shown
in a third frame in the "top-bar". That frame will have the JavaScript
reference "top.menu" in substitute for the left menu and is made by
the script "alt\_menu\_sel.php".

So setting the user profile like this...

|img-15|

... will yield this result for backend menu navigation:

|img-16|

#. (alt\_toplogo.php)

#. alt\_menu\_sel.php: Basically a simple document with a selectorbox. An
   "onchange" event is fired when an item is selected. The onchange-event
   will simply call the function "top.goToModule(' *module\_name* ')" in
   order to change module - so in reality it's all handled in the main
   frameset as with the other types of menus which also call the function
   in the frameset.

#. (alt\_topmenu\_dummy.php)


Alternative menu: Icons in top frame
""""""""""""""""""""""""""""""""""""

You can also have the menu as a list of icons in the top frame. This
obviously requires you to know the menu items by heart so you can
recognize the items on their icons only without the descriptive
labels:

|img-17|

... and the menu will look like:

|img-18|


Main- and sub modules
"""""""""""""""""""""

Basically there are two types of modules,  *main* modules and  *sub*
modules. Normally we refer to them just as "modules" or "backend
modules".

The term "modules" is used within TYPO3 specifically for these backend
modules. For the frontend we might also like to call a message board
or guest book for "a module". However to distinguish between the two
worlds we use another term, "plugins", for frontend applications such
as message boards, shops, guest books etc.

Modules are discussed in detail later in this document. For now just
observe the distinction between main- and submodules:

**Main modules** are those on the "first level" in the menu. Most of
them are not linking directly to any script but are merely "headlines"
for the submodules under them. One exception is the "Doc" module which
*is* linked to the alt\_doc.php script.

|img-19|

**Sub modules** are those on the second level in the menu. As such
they  *don't have to* have any technical relationship with the main
module. The main module might simply act as a category for the module.
However for "Frameset modules" it's a little different (see next
section). Sub-modules may be named "Web > List" or "User > Setup" but we
encourage unambiguous naming of modules so any module can be referred
to by its own name only, eg. "List module" (Web >  **List** ) or
"Filelist module" (File >  **Filelist** ) - it turns out to be much
easier to say in words " *The filelist module* " than " *The File-
Filelist module* ".

|img-20|

Finally  **"Function menus"** are what you get when you create backend
modules "on the third level" - basically a module which inserts itself
into a menu of an existing main- or sub-module. This of course
requires the host module to supply an API for that, but that is in
fact the case with both the "Info" and "Functions" modules!

In this example the extension "info\_pagetsconfig" has been loaded in
the EM (Extension Manager) and thus the Info module will show this
item in the menu:

|img-21|


Frameset Modules
""""""""""""""""

Main modules can be configured to load a frameset into the content
frame instead of the modules default script. This is the case of the
Web and File main modules. In itself that might sound trivial but the
point is that "Frameset modules" are more than just a "category" for
submodules - they are offering additional features:

In the case of frameset modules the idea becomes clear when you
observe the usage; Both the Web and File main modules offers a two-
split window with a page/folder tree on the left and a  *sub-module*
script loaded in the right frame. The point is that a click in the
left frame will load the sub-module script in the right frame  *with*
an  *&id=* parameter! In the case of the Web module this "id" is of
course the page id, for the File module it's the path to the directory
that should be shown.

Still this could be achieved by a local frameset made by the module
itself, but the main point is that even if you switch between the sub-
modules in the menu the id-value is passed along to the other sub-
module and further will the id be restored and sent to the script when
a totally other module has been accessed in the meantime and the user
goes back to one of the sub-modules within the frameset module.

For instance you might click the page "A page title" below, the List
module will show the records for that page id, then you go the the
Extension Manager and when you later click on the List, Info, Access
or Functions sub-module the last page id displayed will be shown
again.

That is what a Frameset module does.

(See the module section for details on how to configure such a module)

|img-22|

A Frameset Module consists of these scripts:

#. alt\_mod\_frameset.php: The frameset is constructed by this script for
   *all frameset modules* . This script will receive information about
   the scripts to load in the frames inside.

#. [ *frameset module specific script name* ]: Navigation script as
   specified in the module configuration of the Frameset Module. (JS
   reference: top.content.nav\_frame)

#. border.html: A simple vertical bar separating the two main frames. (JS
   reference: top.content.border\_frame)

#. [ *module specific script name* ]: Sub-module script as specified in
   the module configuration of the sub-module. (JS reference:
   top.content.list\_frame)

Certain requirements are put on the function of the navigation and
sub-module scripts in order to ensure complete compatibility with the
concept of Frameset Modules. This is basically about updating some
JavaScript variables in the main frameset. See the module section for
more details.


Condensed Mode
""""""""""""""

|img-23|

If Condensed Mode is enabled for the user it has an impact on how
Frameset Modules handles the splitting of the screen into navigation
and list frame. Basically the frameset is not used and the
communication goes always from menu -> navigation frame -> list frame:

|img-24|

This mode is designed to help people with small screen resolutions to
keep all the information on the screen without having to scroll
horizontally (too much). In default mode TYPO3 runs best at
resolutions of 1024x768 or above.

