Getting started
===============

This Term you will be developing programs in Python using multiple
text files, editors, the command-line, and version control. This is
the usual way of creating programs, especially for larger software
libraries. To help you, a skeleton repository in which some tasks have
already been completed is provided as a starting point.

To get started:

#. Read the :ref:`Requirements` section.

#. Install and configure your development environment (see
   `Development environment`_).

#. Create a Git repository for your project (see `Create a development
   repository`_) from the provided template.

#. Read the :ref:`Deliverables` section, and within your team consider
   dependencies between 'tasks' in the deliverables and allocate
   independent tasks to a team member (see `Project planning`_).

#. Read :ref:`using-git`.

#. Start implementing your tasks (see `Using Anaconda`_).

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

   Experienced programmers have their favourite tools and development
   environments. If you are experienced with Git, running Python and
   using editors, you are free to use your preferred tools.

   The following procedures and tools are suggested for less
   experienced programmers.


Software installation
^^^^^^^^^^^^^^^^^^^^^

The following instructions are for installing the necessary tools on
your own computer, and are common for Linux distributions, macOS and
Windows. The tools are already installed on the computers in the DPO.

#. Download the Anaconda environment
   (https://www.continuum.io/downloads) and install. Select the Python
   3 version for download.

#. Download and install Git (https://git-scm.com/downloads). The
   default installation options are suitable.


Command line terminal
^^^^^^^^^^^^^^^^^^^^^

Some of the following requires a command line terminal. To open a
command line terminal:

- Linux: Open a 'Terminal' (from DPO use ``Programming`` -> ``Anaconda
  Shell``).
- macOS: Open a 'Terminal'
- Windows: Launch 'Anaconda Prompt' or 'Git Bash'.



Git user configuration
^^^^^^^^^^^^^^^^^^^^^^

To configure Git with your name and email address, open a
terminal/command prompt and use the commands:

.. code-block:: bash

   $ git config --global user.name "John Doe"
   $ git config --global user.email johndoe@example.com

You will need to configure Git on each computer that you use.


Testing your Python installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note::

   In the DPO, 'Anaconda Navigator' and 'Anaconda Shell' can launched
   from the 'Programming' menu. Use 'Anaconda Shell' rather than a
   regular terminal as it is configured for Anaconda Python.

#. Open the 'Anaconda Navigator' program.
#. From Anaconda Navigator, launch Spyder.
#. Create a new file in Spyder, and enter some simple Python code,
   e.g.::

     print("Testing Python install")

#. Run the test program (``Run`` -> ``Run``). The output of your
   program should appear in the Spyder console window.

.. tip::

   By default, Spyder runs Python scripts within the same Python
   console. Variables will persist between subsequent runs of
   different scripts; this can lead to confusion.

   It is recommended to run in a new console each time. To make this
   the default follow: ``Tools`` -> ``Preferences`` -> ``Run`` and
   select 'Execute in a new dedicated Python console'.


Create a development repository
-------------------------------

You are required to use Git in this activity.  It is strongly
recommended that you use a hosted Git service, such as `Bitbucket
<https://bitbucket.org/>`__, `GitHub <https://github.com/>`_, or
`GitLab <https://about.gitlab.com/>`_.

If you are unfamiliar with these services, use `Bitbucket
<https://bitbucket.org/>`__. The following instructions are for
Bitbucket and novice users. If you are an experienced Git user you
will likely have your own workflow.

#. Create an account on Bitbucket and login. Share your username with
   your team member.

#. One team member should create a copy ('fork') of the starter code
   by going to:

   https://bitbucket.org/CUED/partia-flood-warning-system/fork

   a. Tick the box 'This is a private repository'.

   #. From the overview page
      (https://bitbucket.org/dashboard/overview) you should see your
      repository. Click on it.

   #. On your repository page, click 'Share' and enter the username of
      your project partner give them 'write' or 'admin' access.

#. Check that you can see the repository at
   https://bitbucket.org/dashboard/repositories.

#. On the repository page, from the menu on the left-hand side of
   click 'Clone' and copy the command.  Use this command in a terminal
   to clone a copy of the repository to your computer, e.g.:

   .. code-block:: bash

      git clone https://jane-doe@bitbucket.org/john-doe/partia-flood-warning-system.git

   You should now have a local (on your computer) copy of the code.

#. From the terminal, enter the code directory attempt to execute file
   ``Task1A.py``:

   .. code-block:: bash

     python Task1A.py

   (on some systems you may need to use ``python3 Task1A.py``).

   You should see some output on river level monitoring stations.

.. note::

   The Python code from which you will start uses some modules
   (``requests`` and ``dateutil``) that are not part of the Python
   standard library, but which are distributed as part of Anaconda.
   If you see an error that a module is missing, you can install the
   module using ``pip``. Use:

   .. code-block:: bash

      pip install requests --user
      pip install python-dateutil --user

   Depending on your system, you may need to replace ``pip`` by
   ``pip3``.

You can repeat these instruction on as many computers as you wish. An
advantage of using version control (Git) is that it is easy to move
between computers.


Project planning
----------------

#. Examine the first few project deliverables, and divide independent
   tasks amongst team members. Each team member can then work on tasks
   independently.
#. Communicate frequently with team members to update them on your
   progress, and seek help from a team member if required.
#. As tasks are completed, you may want to review each others work and
   provide feedback.
#. As you progress through the tasks, periodically assess which tasks
   are independent and allocate these to a team member.


Using Anaconda
--------------

These instructions are for using the Anaconda Python environment.

#. Launch Spyder and navigate to your code repository.
#. Open/create the files you wish to edit. 'Module' files should go in
   the directory ``floodsystem/``. The ``Task*.py`` files should go in
   the root directory of the repository.
#. Use the Spyder menu to 'run' your programs.

As you develop you programs, commit your changes (using Git) and push
these to the main repository. If you are unsure how often to commit
and push changes, err on the side of committing and pushing more
frequently rather than less frequently. *Commit at least upon the
completion of each task.*
