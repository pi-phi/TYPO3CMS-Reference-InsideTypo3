.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Clipboard
^^^^^^^^^

The basic engine behind copying and moving elements around in TYPO3 is
the clipboard (t3lib/class.t3lib\_clipboard.php). The clipboard simply
registers a reference to the element(s) (file or database record) put
on the clipboard. The clipboard is saved in the session data and
normally lasts for the login session.

The clipboard content can be seen in the Web>List module if you enable
"Show clipboard":

|img-147|

The clipboard has multiple "pads", a "Normal" pad an a series of
"numeric pads" named "Clipboard #xxx".

- The "Normal" pad can contain one element at a time. The element is
  registered for "copy" or "cut" operation (depending on the function
  that selected it for the clipboard). The "Normal" pad is always used
  from the CSM (Context Sensitive Menu) elements.The "Normal" pad is
  used for most standard copy/cut/paste operations you need.

- The numeric pads can contain multiple elements, even mixed between
  database elements and files/folders. Registering elements to a numeric
  pad is done from the Web>List or File>Filelist modules when they are
  in the "Extended view" mode and a numeric pad is enabled. "Copy" or
  "Cut" mode is toggled for the whole selection by a button on the
  clipboard.The "Numeric pads" are used for advanced needs where
  typically many elements has to be copied/moved in one operation.


The "Normal" pad
""""""""""""""""

When you are using the CSMs to copy/cut/paste elements around you will
automatically use the Normal pad on the clipboard. Internally that is
where TYPO3 registers the element.

In the CSM you always have a "Cut" and "Copy" option and depending on
the context you might also have "Paste into" and "Paste after".

- "Paste into" equals the normal "Paste" operation from a file system;
  it will paste the element  *into* the file folder / page you pointed
  to.

- "Paste after" is special for TYPO3s page tree or record lists where
  elements might be arranged in a special order. In that case you need a
  function like "Paste after" which can insert an element  *below* the
  element you clicked in a list of manually ordered items.

|img-148|

In the screenshot above you can see the clipboard related options from
the CSM of a page in the page tree.

Below you can see how the File>Filelist module looks when a file is
selected on the clipboard. First of all you will get a visual response
from the "copy" icon if the current element is the one already
selected. You can deselect by selecting "Copy" again. Also you will
see that the File>Filelist module (as well as the Web>List module)
provides copy/cut/paste icons directly in the list. Finally, notice
the clipboard which is opened in the bottom of the list. It shows the
selected element and which mode ("Copy" or "Cut") it is selected in.


|img-149|
"""""""""


The numerical pads
""""""""""""""""""

To select elements to the numeric pads you have to use the
File>Filelist or Web>List modules, enable the clipboard and select one
of the numeric pads. In the file or record lists you can now tick off
which elements to select and click the "Select" icon to move the
selection to the clipboard:

|img-150|

The screen will be reloaded and the selected elements shown in both
the list and the open clipboard:

|img-151|

Paste operations are done by the paste icons provided in the list.

Notice that in this case three files are also on the same pad. This is
allowed but obviously they will not be possible to paste where
database records can be pasted - an vice versa.

In the File>Filelist module you will see that the files are the active
elements if you go there:

|img-152|


Thumbnails and "Copy" / "Cut" modes
"""""""""""""""""""""""""""""""""""

The clipboard has controls to enable thumbnail display for image
files:

|img-153|

You can also switch between "Copy" and "Cut" modes. This is necessary
particularly when operating on the numeric pads:

|img-154|


Accessing clipboard content from PHP
""""""""""""""""""""""""""""""""""""

In "TYPO3 Core API" there is an `example of how you can access
elements registered on the clipboard
<#Accessing%20the%20clipboard%7Coutline>`_ .

