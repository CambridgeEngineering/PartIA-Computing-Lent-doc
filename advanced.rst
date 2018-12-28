Suggestions for advanced developers
===================================

These development topics are optional, but are suggested for those who
are already experienced with Git and Python and those who wish to
develop their skills further.

.. topic:: Branching with Git and merge request

   Use a Git *branch* for each task, and merge your topic branch into
   ``master`` once it is complete and tests pass. Use merge requests
   to merge code into the ``master`` branch.


.. topic:: Code style

   Use `flake8 <http://flake8.pycqa.org/>`__ for static analysis and to
   check your code for style.


.. topic:: Test coverage

   Check your test coverage using `pytest-cov
   <http://pytest-cov.readthedocs.io/>`__.


.. topic:: Installing the module and using from a Jupyter notebook

   The template repository has a ``setup.py`` file which allows the
   ``floodsystem`` module to be installed. Install the module from the
   project directory using:

   .. code-block:: bash

      pip install . --user

   If your system also has Python 2 installed, you may need to use:

   .. code-block:: bash

      pip3 install . --user

   Once the module has been installed, you should be able to import it
   from any location. Try using your module from a Jupyter notebook.
