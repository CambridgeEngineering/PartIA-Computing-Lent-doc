Getting started
===============

.. You will be developing programs in Python using multiple files, editors,
  the command-line, and version control. This is the usual way of
  creating *libraries*, especially for larger projects. To help you
  start, a skeleton repository in which some tasks have already been
  completed is provided as a starting point.

.. To get started:

#. Read the :ref:`Requirements` section.

#. Install, configure and test your development environment
   (`Development environment`_).

#. Create a Git repository for your team/project (`Creating a team
   development repository`_) from the provided template.

#. Read :ref:`using-git`.

#. Read the :ref:`Deliverables` section, and with your team consider
   dependencies between 'tasks' in the deliverables and allocate
   independent tasks to a team member (`Project planning`_).

#. Start implementing your tasks (`Editing and executing Python code`_).

.. tip::

  Start simple and work in small steps. It is much easier to add
  functionality to a working program than to fix a complicated
  non-working program.

.. note::

  When developing your programs, you may need to review the activity
  notebooks from Michaelmas Term.


.. _development_environment:

Development environment
-----------------------

.. note::

   Experienced developers have their preferred tools and development
   environments. If you are experienced with Git, Python and using
   editors, you are free to use your preferred tools.

   The following procedures and tools are suggested.


Option 1: Web-based environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can use GitHub Codespaces, which provides a development environment
in your browser.


Option 2: Local software installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Install Visual Studio Code (https://code.visualstudio.com/).

   Visual Studio Code will provide instructions on how to install
   ``git`` and ``python`` when you need them. Otherwise, instructions at
   https://code.visualstudio.com/docs/sourcecontrol/overview and
   https://code.visualstudio.com/docs/languages/python.


Testing your Python installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Create a file in VS Code with the extension ``.py`` and enter
   some simple Python code, e.g.::

     print("Testing Python install")

#. Click the 'play' button at the top of the open file.


.. _creating-and-sharing:

Creating a team development repository
--------------------------------------

#. Log into GitHub (create an account using your @cam.ac.uk email
   address, or use any other GitHub account you wish).

#. **One team member only:** The template start code is at
   https://github.com/CambridgeEngineering/PartIA-Flood-Warning-System.
   Click on the green "Use this template" button, select "Create a new
   repository" give your new repository a name. Make your repository
   "private". In the "Settings" section for your repository add your
   team members as "Collaborators" and share the name of the repository
   with team members.

#. Clone your team's repository using VS Code "Source control".

#. From VS Code, execute file ``Task1A.py``. You should see some output
   on river level monitoring stations.

.. note::

   The Python code uses some modules (``requests`` and ``dateutil``)
   that are not part of the Python standard library. If you see an error
   that a module is missing, you can install the module using ``pip``.
   Use:

   .. code-block:: bash

     py -m pip install requests python-dateutil

   in the terminal window.


Editing and executing Python code
---------------------------------

#. Launch VS Code and open your local code repository directory.

#. Open/create the files you wish to edit. 'Module' files should go in
   the directory ``floodsystem/``. The ``Task*.py`` files should go in
   the root directory of the repository.

#. Use right-click -> 'Run Python File in Terminal' on the program text
   in VS Code to run the Python code.

As you develop you programs, commit your changes (using Git) and push
these to your shared online repository. If you are unsure how often to
commit and push changes, err on the side of committing and pushing
frequently. *Commit at least upon the completion of each task.*


.. _continuous-integration:

Automated testing
-----------------

The starter template repository includes the file
``.github/workflows/pythonapp.yml`` which configures automated testing,
known as *continuous integration* (CI), on GitHub. Against each commit
you will see on the GitHub repository page whether or not the tests are
passing.

Edit ``.github/workflows/pythonapp.yml`` to run your deliverables in the
test system and to add code tests to your test suite.


Project planning
----------------

#. Examine the first few project deliverables, and divide independent
   tasks amongst team members. Each team member can then work on tasks
   independently.

#. Communicate frequently with team members to update them on your
   progress, and seek help from a team member if required.

#. As tasks are completed review each others work and provide feedback.

#. As you progress through the tasks, periodically assess which tasks
   are independent and allocate these to a team member.
