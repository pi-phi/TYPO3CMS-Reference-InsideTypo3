.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


Workspaces
^^^^^^^^^^


Problems with versioning usability
""""""""""""""""""""""""""""""""""

One problem with raw versioning is that it easily requires a lot of
administration and awareness from users. For instance, an author has
to consciously create a new version of a page or content element
before he must edit it. Maybe he forgets. So either he makes a change
live or - if TYPO3 is configured for it - he will be denied access to
editing but frustrated over an error message. Further, keeping track
of versions across the system might be difficult since changes are
often made at various places and should be published together.

Some of these problems are fixed when elements are always processed
with a workflow that keeps track of them. But a workflow process might
be too rigid for scenarios where a group of editors are concerned with
the site content broadly and not the narrow scope of an element
centred workflow.

Furthermore, the preview of future content is hard to implement unless
you require people to request a preview of each individual new version
- but most often they like to see the combined impact of all future
versions!


The perfect solution
""""""""""""""""""""

The concept of workspaces is the answer. Workspaces puts versioning
into action in a very usable and transparent way offering all the
flexibility from live editing but without sacrificing the important
control of content publishing and review.

A workspace is a state in the backend of TYPO3. Basically there are
three types of workspaces:

- LIVE workspace: This is exactly the state TYPO3 has always been in.
  Any change you make will be instantly live. Nothing has changed, it
  just got a name.

- Draft workspace: When a user selects the draft workspace new rules
  apply to anything he does in the backend:

  - Draft: Any change he tries to make will not affect the live website.
    It's a safe playground.

  - Transparent versioning: He can edit pages and elements because a new
    version is made automatically and attached to the workspace. No
    training needed, no administrative overhead!

  - Previewing: Visiting the frontend website will display it as it will
    appear when all versions in the workspace is eventually published
    (switch enable/disable this feature).

  - Overview of changes: The workspace manager module gives a clear
    overview of all changes that has been made inside the workspace across
    the site. This gives unparalleled control before publishing the
    content live.

  - Constraints: Only tables that support versioning can be edited. All
    management of files in fileadmin/ is disabled because they may affect
    the live website and thus would break the principle of “safe
    playground”.

- Custom workspaces:

  - Inherits all properties of the default “Draft workspace” but can be
    configured additionally with owners, members and reviewers plus
    database- and file mounts plus other settings. A custom workspace is a
    great way to do team-based maintenance of (a section of) the website
    including a basic implementation of workflow states with editor-
    reviewer-publisher.

  - Some of the constraints of the default draft workspace can be eased up
    a bit by configuration; For instance records that does not support
    versioning can be allowed to be edited and file mounts can be defined
    inside of which files  *can* be managed.

A draft workspace is a container for draft versions of content. Each
versionable element can have zero or 1 version in a workspace
(versions are attached to workspaces with a relation in the field
“t3ver\_wsid”). The fact that there can be only one new version of any
element in a draft workspace makes in unambiguous which version to
edit, preview and publish.

**Analogy:** The concept of workspaces can be compared with how CVS
works for programmers; You check out the current source to your local
computer (= entering a draft workspace), then you can change any
script you like on your local computer (= transparent editing in the
workspace), run tests of the changed code scripts (= previewing the
workspace in the frontend) , compare the changes you made with the
source in CVS (= using the Workspace Manager modules overview to
review the complete amount of changes made) and eventually you commit
the changes to CVS (= publishing the content of the workspace).


Publishing and swapping
"""""""""""""""""""""""

There are two ways to publish an element in a workspace; publish or
swap. In both cases the draft content is published live. But when
swapping it means the current live element is attached to the
workspace when taken offline. This is contrary to the publish mode
which pushes the live item out of any workspace and “into the
archive”.

The swapping mode is useful if you have a temporary campaign, say a
christmas special frontpage and website section. You create the
christmas edition in a custom workspace and two weeks before christmas
you swap in the christmas edition. All normal pages and elements that
were unpublished are now in the workspace, waiting for christmas to
pass by and eventually the old frontpage etc. will be swapped back in.
The christmas edition is now back in the workspace and ready for next
year.


More on Workspace types
"""""""""""""""""""""""

I would like to more clearly describe the various workspace types,
their differences and applications:

.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Topic
         Topic

   Live workspace
         Live workspace

   Draft workspace (default)
         Draft workspace (default)

   Custom workspaces
         Custom workspaces


.. container:: table-row

   Topic
         **Access**

   Live workspace
         Users and groups must be specifically allowed access to the Live
         workspace.

         (Checkboxes in user/group record)

         *(For upgrades from pre-4.0 versions this is done by default).*

   Draft workspace (default)
         Users and groups must be specifically allowed access to the Draft
         workspace.

         (Checkboxes in user/group record)

   Custom workspaces
         Granted through the workspace configuration which includes:

         \- A list of editors (users and/or groups)

         \- A list of reviewers (users and/or groups)

         \- Owner users (initial creator)


.. container:: table-row

   Topic
         **Editing**

   Live workspace
         Live content

   Draft workspace (default)
         Draft versions of live content

   Custom workspaces
         Draft versions of live content

         *Option: To allow editing of tables without versioning available.*


.. container:: table-row

   Topic
         **DB mounts**

   Live workspace
         From user profile

   Draft workspace (default)
         From user profile

   Custom workspaces
         Specific DB mounts can be specified in which case they will overrule
         DB mounts from user profiles.

         Specific DB mounts are required to be within the DB mounts from the
         user profile (for security reasons)

         If no DB mounts specified for workspace, user profile mounts are used
         (default)


.. container:: table-row

   Topic
         **File mounts**

   Live workspace
         From user profile

   Draft workspace (default)
         None available. All file manipulation access is banned! (Otherwise
         violation of “draft principle”)

   Custom workspaces
         By default, none is available due to same principle as for Draft
         workspace.

         Optionally, file mounts can be specified for convenience reasons.


.. container:: table-row

   Topic
         **Scheduled publishing**

   Live workspace
         N/A

   Draft workspace (default)
         N/A

   Custom workspaces
         If CLI-script is configured in cronjob you can specify publishing
         date/time down to the minute. You can also specify an unpublish time
         which requires the use of swapping as publishing type.


.. container:: table-row

   Topic
         **Reviewing**

   Live workspace
         Only through a separate workflow system.

   Draft workspace (default)
         Content can be raised from “Editing” stage through “Review” to
         “Publish”.

         However, the state does not impose any limitations on editing and
         publication of workspace contents.

   Custom workspaces
         **Members** can raise content from “Editing” stage to “Review”.
         Members can only edit content when its in “Editing stage” (or
         “Rejected”)

         **Reviewers** can raise the content from “Editing” stage to “Review”
         stage to “Publish” - or they can reject content back to editing.
         Reviewers can only edit content in these modes.

         **Owners** can operate all states of course. Owners are the only ones
         to edit content when in “Publish” mode. Thus “Publish” mode provides
         protection for content awaiting publication.

         The “Rejected” flag is reset automatically when editing occurs on a
         rejected element.

         Options available for automatic email notification between the roles.


.. container:: table-row

   Topic
         **Publishing**

         (For all: Requires edit access to live element)

   Live workspace
         No limitations. Content can be edited live and even content from other
         workspaces can be published through the versioning API regardless of
         stage.

   Draft workspace (default)
         All users with access to Live workspace is able to publish.

   Custom workspaces
         Workspace owners can publish (even without access to Live workspace).

         Reviewers/Members cannot publish  *unless* they have access to online
         workspace as well (this default behaviour can be disabled).

         Option: Restrict publishing to elements in "Publish" stage only.


.. container:: table-row

   Topic
         **Settings**

   Live workspace
         N/A

   Draft workspace (default)
         N/A

   Custom workspaces
         Users with permission to create a custom workspace can do so.

         Workspace owners can add other owners, reviewers and editors and
         change all workspace properties.


.. container:: table-row

   Topic
         **Auto versioning**

   Live workspace
         N/A

   Draft workspace (default)
         Yes

   Custom workspaces
         Yes, but can be disabled so a conscious versioning actions is
         required.


.. container:: table-row

   Topic
         **Swapping**

   Live workspace
         N/A

   Draft workspace (default)
         Yes

   Custom workspaces
         Yes, but can be disabled.


.. container:: table-row

   Topic
         **Versioning types**

   Live workspace
         All

   Draft workspace (default)
         All

   Custom workspaces
         All, but you can disable any of the types “Element”, “Page” and
         “Branch”.


.. container:: table-row

   Topic
         **Other notes**

   Live workspace


   Draft workspace (default)


   Custom workspaces
         Custom workspaces has a freeze flag that will shut down any
         update/edit/copy/move/delete etc. command in the workspace until it is
         unset again.


.. container:: table-row

   Topic
         **Module access**

   Live workspace
         All backend modules can specify $MCONF['workspaces'] =
         “[online,offline,custom]” to limit access based current workspace of
         user. See description elsewhere in this document.


.. container:: table-row

   Topic
         **Usage**

   Live workspace
         Administrative purposes. First creation of site.

   Draft workspace (default)
         Everyday maintenance for trusted editors.

   Custom workspaces
         Specific projects on a site branch. Simple review-cycles. Informal
         team-work on site maintenance.


.. ###### END~OF~TABLE ######

Generally, “admin” users have access to all functionality as usual.


Supporting workspaces in extensions
"""""""""""""""""""""""""""""""""""

Since workspaces implies transparent support all over the backend and
frontend it means that extensions must be programmed with this in
mind. Although the ideal is complete transparency in backend and
perfect previews in the frontend this is almost impossible to obtain.
But a high level of consistency can be obtained by using API functions
in TYPO3. These functions and the challenges they are invented to
answer are discussed in “TYPO3 Core API”.

