Development tools and practices
===============================


Working in a team
-----------------

Most software is developed in teams, and working effectively in a
development team requires certain skills and practices. At a planning
level:

- Examine the required tasks, then discuss and decide on the
  dependencies between tasks. To start, allocate independent tasks to
  team members.

- Let your team know when a task or piece of functionality is
  complete.

- Discuss frequently.


At the implementation level:

- Use a version control system, such as Git. With Git:

  - Work that is committed cannot be lost (unless you try really
    hard) - your team members cannot accidentally delete your code.

  - Commit changes frequently and in small chunks. This makes clear to
    others what you are working on, and any conflicts will be easier to
    resolve.

  - It is easy to switch between computers.

- Add tests as functionality is developed. This:

  - Builds confidence that your implementation is correct.

  - Can detect if a change by you or a team member has affected your
    implementations. (One of the most frustrating situations in team
    development is when a change by another team members breaks your
    carefully constructed functionality.)


.. _using-git:

Using Git
---------

`Git <https://git-scm.com/>`_ is modern widely used *version control
system* (VCS). A version control system tracks changes to source code.
It can show what has changed, and who has made changes. Git is very
powerful and has many features. Elementary Git usage for getting started
is summarised below.


Creating or cloning a repository
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To clone a repository (typically hosted by an online service):

.. code-block:: bash

   git clone https://gitlab.com/CUED/partia-flood-warning-system.git

The location for a particular repository can be found on the online
repository page.

To create a new repository, create a directory and execute in the
directory the command:

.. code-block:: bash

   git init



Adding a new file or adding file changes to the staging area
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The command:

.. code-block:: bash

   git add myfile.py

instructs Git that we want to track the file ``myfile.py``, or if the
file is already tracked that we will want to add any changes to the
repository.


Committing changes to the project history
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``commit`` command commits changes to the project history, and each
commit has a 'commit message' associated with it:

.. code-block:: bash

   git commit -m "Complete Task 1C"

It is possible at any time to see the changes between any two commits,
and to revert a repository to a particular commit.


Collaborating: merging changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To fetch remote changes into your repository, e.g. changes made by your
team mate:

.. code-block:: bash

   git pull

In general, you should ``commit`` your changes before using ``pull``.


To send your changes to the remote server:

.. code-block:: bash

   git push

If team members have 'pushed' changes, you will need to use ``git pull``
before you can push. Once you have pushed changes, other team members
will receive your changes when they next 'pull'.


Seeing changes in your working directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The command:

.. code-block:: bash

   git diff


shows any changes to your code since the last commit. The command:

.. code-block:: bash

   git status

will show any changes to files that are (a) tracked but have changed
since the most recent commit, and (b) files that are not tracked (have
not been added using ``git add``).


Project history
^^^^^^^^^^^^^^^

The log of project commits is displayed by the command:

.. code-block:: bash

   git log

The output will include the commit messages and the author of each
commit.

Project history is shown by online services, like GitLab, and this the
simplest way to examine project change. It is also possible to add
comments and suggestions on particular code changes to discuss with team
members.


How often should I commit changes?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Often. Structure your work into small chunks, and commit after
completing each 'chunk'. At the very least, you should commit changes at
the completion of each *Task* in the *Deliverables* section.

Also, pull and push frequently.


Getting help with Git
^^^^^^^^^^^^^^^^^^^^^

There are many online resources for learning Git, and search engines for
very useful.  Helpful tutorials for beginners are:

- https://www.codecademy.com/learn/learn-git
- https://try.github.io
- https://swcarpentry.github.io/git-novice/
- https://docs.gitlab.com/ee/gitlab-basics/
- https://www.atlassian.com/git/tutorials/


.. _using-pytest:

Test framework
--------------

Testing is critical for high quality software development, and there are
many tools for helping with this. In this project you will use `pytest
<http://docs.pytest.org/>`__.  Some tests are in the project starter
repository.

Write tests as you go, and run the tests frequently to check that
nothing has been inadvertently broken.


Running tests
^^^^^^^^^^^^^

pytest is very simple to use:

#. Put tests in files starting with ``test_``, e.g. ``test_data.py``.

#. In the test file, prefix test function with ``test_``, e.g.::

     def test_sum():
         a, b = 2, 3
         assert a + b == 5

#. To run all tests in all ``test_*.py`` files in a directory, use:

   .. code-block:: bash

      py.test .

   To run all test in the file ``test_data,py``:

   .. code-block:: bash

      py.test test_data.py

   pytest will print a summary of the number of tests run, with the
   number that pass and the number that fail.

If you are working on a computer that has Python 2 and Python 3
installed, depending on your configuration you may need to use:

.. code-block:: bash

   python3 -m pytest test_data.py

to run the tests.


Writing tests
^^^^^^^^^^^^^

Aim to have at least one test for every function in your library. Some
tests will just check that a function can be called successfully, e.g.::

  import mymodule

  def test_call():
      x = mymodule.do_something(4)

More useful test will check results, e.g.::

    import mymodule

    def test_my_sum():
        sum = mymodule.sum(7, -8)
        assert sum == -1

Take care when comparing floating point values, since round-off errors
can make precise comparison difficult. Use rounding to compare floats,
e.g::

    import math

    def test_math_sine():

        x = math.sin(0.0)
        assert round(x, 8) == 0  # 'round' keep 8 digits after the decimal point

        pi = 3.14159265359
        x = math.sin(pi)
        assert round(x, 8) == 0

        pi = 3.14159265359
        x = math.sin(pi/2.0)
        assert round(x - 1, 8) == 0
