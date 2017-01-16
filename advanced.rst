Suggestions for advanced developers
===================================

These development topics are optional, but are suggested for those who
are already experienced with Git and Python and those who wish to
develop their computing knowledge further.

.. topic:: Branching with Git

   Use a Git branch for each topic, and merge your topic branch into
   ``master`` once it is complete. See
   https://www.atlassian.com/git/tutorials/using-branches for
   information on branching.


.. topic:: Code style

   Use `flake8 <http://flake8.pycqa.org/>`__ to check your code for
   style.


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
