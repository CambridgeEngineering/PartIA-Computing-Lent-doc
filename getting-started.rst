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

Software installation
~~~~~~~~~~~~~~~~~~~~~~

#. Install Visual Studio Code (https://code.visualstudio.com/).

#. Install Python following the instructions at
   https://code.visualstudio.com/docs/languages/python.

#. Install git following the instructions at
   https://code.visualstudio.com/docs/sourcecontrol/overview.


Testing your Python installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Create a file in VS Code with the extension ``.py`` and enter
   some simple Python code, e.g.::

     print("Testing Python install")

#. Right-click from VS Code on the file and select `Run Python File in
   Terminal`. The output of your program should appear in a terminal
   window inside VS Code.


.. _creating-and-sharing:

Creating a team development repository
--------------------------------------

#. Log into GitHub (create an account using your @cam.ac.uk email
   address, or use any other GitHub account you wish). The template
   start code is at
   https://github.com/CambridgeEngineering/PartIA-Flood-Warning-System.
   Click on the green "Use this template" button, give it a name, and
   create your new project. Since you will be collaborating within the
   lab group, create only *one* new project for your lab group. It does
   not matter whose GitHub account is used.

   The next step (below) should then be done by each member of the team,
   accessing the *same* project on github.com. This is how you will be
   sharing code.

#. Fetch a local copy of your repository by *cloning* it. The 'Code -> Clone'
   button on the GitHub page for your repository gives the address of
   your Git repository. From a terminal::

     git clone <address of my repository>

   You should now have a local (on your computer) copy of the code. If you use VS Code, you
   can clone using the three-dots menu under the Source Control tab.



.. _creating-and-sharing:

Creating a team development repository
--------------------------------------

#. Log into GitHub (create an account using your @cam.ac.uk email address,
   or use any other GitHub account you wish). The template start code is at
   https://github.com/CambridgeEngineering/PartIA-Flood-Warning-System, click on the green
   "Use this template" button, give it a name, and create your new project. Since you will
   be collaborating within the lab group, creat only *one* new project for your lab group, it
   does not matter whose GitHub account this happens under. The next step (below) should then
   be done by each member of the team, accessing the *same* project on github.com. This is how
   you will be sharing code.

#. Fetch a local copy of your repository by *cloning* it. The 'Code -> Clone'
   button on the GitHub page for your repository gives the address of
   your Git repository. From a terminal::

     git clone <address of my repository>

   You should now have a local (on your computer) copy of the code. If you use VS Code, you
   can clone using the three-dots menu under the Source Control tab.

#. From the terminal, enter the code directory attempt to execute file
   ``Task1A.py``:

   .. code-block:: bash

     python Task1A.py

   (If you are not using Anaconda, on some systems you may need to use
   ``python3 Task1A.py``).

   You should see some output on river level monitoring stations.

.. note::

   The Python code from which you will start uses some modules
   (``requests`` and ``dateutil``) that are not part of the Python
   standard library, but which are distributed as part of Anaconda. If
   you see an error that a module is missing, you can install the module
   using ``pip``. Use:

   .. code-block:: bash

      pip install requests
      pip install python-dateutil


Editing and executing Python code
---------------------------------

#. From Anaconda Navigator launch 'VS Code' and from VS Code open your
   local code repository directory.

#. Open/create the files you wish to edit. 'Module' files should go in
   the directory ``floodsystem/``. The ``Task*.py`` files should go in
   the root directory of the repository.

#. Use right-click -> 'Run Python File in Terminal' on the program text
   in VS Code to run the Python code.

Python code can be run directly from a terminal. In a directory
containing Python code in a file named ``test.py``, it can be be
executed from the terminal using::

   python test.py

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
