.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


Using versioning and workspaces
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section shortly covers the workspace related features in the
backend with a visual tour-de-force.

Most significantly workspaces have a selector box in the lower right
corner of the backend. The shortcut frame is permanently visible for
users unless disabled by Page TSconfig:

|img-92|

In this selector box the backend user chooses between the workspaces
available to him. The whole backend reloads each time he changes
workspace. This is necessary because the backend might be differently
composed depending on the workspace the user is in.

The workspace is reflected in the top of the page tree:

|img-93|

By default the "Live" workspace is not, but this is easily configured
with User TSconfig: "options.pageTree.onlineWorkspaceInfo = 1"

|img-94|

When you are in a draft workspace you will find a "New version" button
in various modules, including Web > Page:

|img-95|

Clicking this button will create a new  **"Page" type version** of the
page. In the page tree "Page" type versions are highlighted with a
blue background color. This means the page header is versioned and
content elements on the page is copied along. (See previously for a
description of this versioning type). This type of versioning offers
the flexibility to rearrange content elements between the columns of a
page.

|img-96|

The module  **Web > Versioning** allows you to monitor the versioning
of elements on a specific page:

|img-97|

This view shows you the live version (sometimes called "Online") and
the draft version (sometimes called "Offline") in a comparison view
which helps you to understand what has changed in the draft version.
You can also raise the stage of the content for review, you can
publish, preview etc.

Instead of explicitly creating a "Page" type version of the page you
can also go ahead and just edit the elements on the page.
*Transparently* an edited element will be versioned and highlighted
with green background to reflect the new state. In the page tree a
page containing versioned elements will be highlighted with light
yellow:

|img-98|

In case you also version the page header it will become green in the
page tree (here I changed the page title to "Sed non tellus"):

|img-99|

Using the Web > Versioning module you will see the workspace content
for the page. Obviously the page and one content element is found in
draft versions in the workspace:

|img-100|

Comparing this view with the previous example where the page was
versioned as a "Page" version you will now see that only changed
elements appear, not every content element from the page. This type is
called  **"Element" versioning** and offers no flexibility in terms of
rearranging element but benefits from maintaining all ids and being
more straight forward to work with.

If you wish to compare changes in the content between the live and
draft version you simply enable "Show difference view" and the display
is updated to this:

|img-101|

This gives a reviewer a clear idea of the changes that has been
performed. The red text is what was removed, the green text is what
was added. A click on the button "Send all to Review" will raise the
"Editing" stage to "Review" stage. "Publish page" / "Swap page" will
perform publishing of all listed elements in the view (unless
restrictions apply which is the case if the individual publish/swap
buttons for each element is missing).

Finally, you can also create a  **"Branch" type version** of the page.
This will copy not only the page and its content elements but the
whole subtree under the page. In order to do so, click the icon of a
page, select "Versioning" and in the "Versioning" view you can create
a new "Branch" version:

|img-102|

The page tree is now updated to look like this. The darker red page is
the root point of the "Branch" version while the lighter red pages is
the individual page tree belonging to that version. This type of
versioning offers the flexibility to rearrange pages in a branch.

|img-103|

The Web > Versioning module displays the "Branch" version like this:

|img-104|

When you deal with "Branch" versions you will find a special token,
#VEP# in the visual page path in backend modules. This token indicates
where the branch point is in the path:

|img-105|

The  **Workspace Manager** is available by clicking the workspace-icon
next to the workspace selector in the lower right corner of the
backend. Or you can access it as the module User > Workspace:

|img-106|

The Workspace Manager is the extended version of "Web > Versioning"
where you will get an overview of the full workspace content. All
versions in the workspace are shown here, can be previewed, managed
and published due to your permissions:

|img-107|

**Previewing content** in the workspace is easy. Generally, you can
enable "Frontend Preview" from the checkbox next to the workspace
selector in the lower right corner of the backend interface. This will
reflect the workspace changes when browsing the frontend website as
long as you are logged in as a backend user.

|img-108|

Alternatively, you use the  **Web > View** module:

|img-109|

Click the page with versioned content in the page tree...

|img-110|

... and you will be able to preview the draft content:

|img-111|

When you see a preview of a workspace in the frontend you will always
be notified by the red box in the bottom of the page:

|img-112|

You can also click the magnifying-glass found many places in the
backend. When you do that in a workspace you will get a special dual-
view of the Live and Draft content combined with access to the Web >
Versioning module for easy approval or publication:

|img-113|

By default you can use the "Draft workspace" for ad-hoc jobs that
doesn't require strict control over review processes etc. In case you
need teams of people with various roles such as author, reviewer and
publisher you can create a  **custom workspace** . By doing so you can
customize roles, permissions and other features to suit your needs:

|img-114|

The custom Workspace is adequately described in the content sensitive
help so no more details will be given here.

The workspace technology offers a simple scheme for  **staging content
through review to publication** . In the Workspace Manager or Web >
Versioning module you can "raise content " to the next level and
attach a comment while doing so:

|img-115|

The stage is raised to "Review" and will be reflected in the
interface:

|img-116|

Likewise you can take the next step to "Publish" at which point the
the workspace owner (of custom workspaces) can uncritically publish
assuming the review process has caught any problems - or the workspace
owner can act as a final level of review:

|img-117|

In case the reviewer or owner finds reasons to reject the content they
can do so with an explanation going to the editor:

|img-118|

At any time a mouse-over on the Stage control will display the log of
events:

|img-119|

**Notice:** The stage feature is only subject to access restrictions
inside custom workspaces. In Live and the default Draft workspace the
feature is available as a state any user can set and final publishing
does not require the "Publish" stage to be reached for any content.

Publishing content from a workspace can either be done with individual
elements, pages including elements or the whole workspace at once.
Publishing the full workspace is available from the top of the
Workspace Manager:

|img-120| |img-121|

For each element in the list you can access  **control buttons** for
*publish, swap, release from workspace, edit element, view change
history* and *preview.*

Next to the control buttons you see the  **Lifecycle** of content. In
the screenshot one of the elements is different from the others: It
turns out that this element has actually been published three times.
This is possible if the "Swap workspace" buttons are used; They will
simply swap the live version with the draft version so that the Live
version is taken back into the workspace in exchange. Doing this a few
times forth and back will increase the lifecycle counter beyond the
otherwise most common state which is "Archive" (published one time).

The other elements shown are all in "Draft" state meaning they have
not been published live - yet.

In the Workspace Manager you can also enable  **display of sub-
elements** for "Page" and "Branch" versioning types:

|img-122|

This will provide you with a threaded display of the versioned
content:

|img-123|

Another feature is to enable  **difference view** in the Workspace
Manager. By doing so you will see every element compared to its live
counterpart (if available) and it will be clear to you what changes
has been made:

|img-124|

|img-125|

The  **system log** will also reflect operations in the workspace. The
"User" column is tagged with the workspace in which the action took
place:

|img-126|

**Setting up access to workspaces:** For the Live and default Draft
workspace you will have to configure this in the Backend User and
Group records by checkboxes:

|img-127|

In the Tools > User Admin module this is also reflected in the
comparison view:

|img-128|

For custom workspaces users are assigned membership directly in the
configuration record of the workspace:

|img-129|

**Tip:** Although the default settings for upgraded websites will be
that all users and groups have access to the Live workspace the
intention of the workspace technology is that in most typical cases
the average backend user only works in a draft workspace and therefore
cannot change live content before a supervisor with access to the Live
workspace will enter the backend and publish the workspace content.

**Creating new content:** The workspace technology is aimed at being
so tough that even a complete website can be built from scratch
without changing any live content. Here the Draft Workspace is used to
build a complete page structure and dummy content. In the workspace
everything looks like if it was live, even when previewed in the
frontend with Web > View.

|img-130|

Changing to the Live workspace reveals a set of placeholder records.
These are necessary to reserve the future position for the new content
in the workspace. However, those placeholders are ignored in the live
workspace frontend and will therefore not affect any live content.

|img-131|

The Web > List module shows the same reflection. In the screenshot
below you can see how pages, content elements, localized versions of
content elements, page language overlays and even TypoScript Templates
are created as versions in the workspace:

|img-132|

In the Live workspace this is reflected like this by the "invisible"
placeholders:

|img-133|

By publication of the workspace these placeholders are substituted
with the new versions from the workspace.

**Managing custom workspaces:** [This section still misses
introduction to the yet missing workspace administration interface in
the Workspace Manager.]

