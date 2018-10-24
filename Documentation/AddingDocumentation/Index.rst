.. include:: ../Includes.txt

.. _Bugfixing-Adding-documentation:
.. _Adding-documentation:

=================
Add documentation
=================

.. rst-class:: horizbuttons-primary-m

- :ref:`h2document:Formatting-with-reST`
- :ref:`h2document:format-rest-cgl`
- :ref:`h2document:rest-common-pitfalls`
- :ref:`h2document:rendering-docs-quickstart`


The documentation `Changelog <https://docs.typo3.org/typo3cms/extensions/core/latest/>`__
and documentation for
`system extensions <https://docs.typo3.org/typo3cms/SystemExtensions/Index.html>`__
is maintained in the core.

.. _changelog:

Document changes (Changelog)
============================

If your change makes it necessary to update the official documentation, you have
to add a .rst (reStructuredText) file describing your change. Not all patches
need an entry in the Changelog. Check the list below. Also see the current
`Changelog <https://docs.typo3.org/typo3cms/extensions/core/latest/>`__
for some examples.

ReST-File-Generator
-------------------

.. tip::

   If you want to save yourself some time you can use the rst Helper at
   https://forger.typo3.org/utility/rst

   Select the type of rst snippet you want to create, enter your issue number
   and click the search button.

When you are done, copy the generated text and create a file with the same
name as suggested in the generator.


Types of changes
----------------

There are four different types of changes
which have to follow a certain format and **always**
need to go into :file:`typo3/sysext/core/Documentation/Changelog/master/`.

Choose one which fits your patch:

.. _documenting-changelog-breaking-changes:

Breaking Changes
~~~~~~~~~~~~~~~~

A patch moved or removed a specific part of core functionality
that may break extensions if they use this part.

**Mandatory sections:**

#. **Description** - why things had to break backwards compatibility.

#. **Impact** - how will the change affect your installation.

#. **Affected Installations** - describe scenarios under which circumstances
   a TYPO3 install will be affected by this change.

#. **Migration** - provide instructions what needs to be done to get things
   working again. Explicitly mention if no migration is possible.


.. _documenting-changelog-deprecations:

Deprecations
~~~~~~~~~~~~

A patch deprecates a certain core functionality
for a planned removal. See more information: :ref:`Deprecations <deprecations>`

**Mandatory sections:**

#. **Description** - why things had to be deprecated.

#. **Impact** - how will the change affect your installation.

#. **Affected Installations** - describe scenarios under which circumstances
   an TYPO3 install will be affected by this change.

#. **Migration** - provide instructions what needs to be done to get things
   working again. Explicitly mention if no migration is possible.


.. _documenting-changelog-features:

Features
~~~~~~~~

A patch adds new functionality.

**Mandatory sections:**

#. **Description** - what can the new feature do.

#. **Impact** - how users are affected by this new feature.


.. _documenting-changelog-important-information:

Important Information
~~~~~~~~~~~~~~~~~~~~~

Anything that does not fit the other categories but is
important enough to require a Changelog entry.

#. **Description** - describe what is so important it needed an rst snippet

.. _changelog-check-rst:

Check your rst file
-------------------

When your change is finished, you can run the following script to check that
your rst file is ok. The script will check all files in
:file:`typo3/sysext/core/Documentation/Changelog`.

::

   Build/Scripts/validateRstFiles.php

This script will check if the .rst files contain all mandatory tags that
are required for the Changelog. It will **not** do a reST syntax check.

In order to make sure that your file contains no syntax errors and will
be rendered correctly, do one or more of the following:

* Check our :ref:`format-rest-cgl` and :ref:`rest-common-pitfalls`.
* Use an editor or IDE that properly supports reST and shows errors
* Render the Changelog locally with docker as explained in the next section


.. _render-the-changelog:

Render the Changelog
--------------------

If you wish to render the Changelog locally, you can use docker as described
in :ref:`h2document:rendering-docs-quickstart`.

First, change to the :file:`core` directory::

   cd typo3/sysext/core/
   source <(docker run --rm t3docs/render-documentation show-shell-commands)
   dockrun_t3rdf makehtml
   open "file:///$(pwd)/Documentation-GENERATED-temp/Result/project/0.0.0/Index.html"
   cd -



.. _documenting-system-extensions:

Document system extensions
==========================

Documentation for system extensions is maintained within a :file:`Documentation`
directory in the respective system extension directory, e.g.
:file:`typo3/sysext/form/Documentation`.

Not all system extensions have their own documentation. Some documentation
(e.g. for the system extension *core*) is maintained within the :ref:`t3coreapi:start`.

If in doubt, ask in the **#typo3-cms-coredev** channel on Slack.

For starting a system extension from scratch, please see
:ref:`h2document:writing-doc-for-ext-from-scratch`.

For an overview of the rendered documentation for system extensions, see
`System Extensions <https://docs.typo3.org/typo3cms/SystemExtensions/Index.html>`__.

When you have made changes to the documentation, you can render
locally with docker to test your changes as described in
:ref:`render-the-changelog`.