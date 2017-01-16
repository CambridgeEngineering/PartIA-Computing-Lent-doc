.. _Requirements:

Requirements
============

This section defines the technical requirements for the
implementation.


Library language
----------------

The library is to be developed in Python 3 and using multiple modules
(files). Each file should collect related functionality.


Code documentation
------------------

Every class, method (a function that belongs to a class) and function
must have a 'docstring'.  The docstring provides an explanation of
what a class or function does. For a function, the docstring should
make clear what the function does, what arguments it expects and what
it returns.  Simple examples of Python docstrings can be viewed `here
<https://en.wikipedia.org/wiki/Docstring#Python>`_.


Development practices
---------------------

The quality of a flood warning software library is paramount;
implementation errors could put lives at risk and lead to substantial
financial losses. You are therefore required to adopt software
engineering best practices. Your team is required to:

- Use the `Git <https://git-scm.com/>`__ version control system (see
  :ref:`using-git`).
- Provide automated tests for your implementations using `pytest
  <http://docs.pytest.org//>`_ to demonstrate the quality of the
  system (see :ref:`using-pytest`)


Data source
-----------

The system is to be built on the (near) real-time river level data at the
nearly 2000 monitoring stations that is made available by the
Department for Environment Food and Rural Affairs (DEFRA) at
https://environment.data.gov.uk/. For most stations river level data
is updated every 15 minutes. The data service is summarised at
https://data.gov.uk/dataset/real-time-and-near-real-time-river-level-data1.

.. note::

   Data is fetched over the Internet using a `REST interface
   <https://en.wikipedia.org/wiki/Representational_state_transfer>`__. With
   a suitably formed URL (a string), as defined in the service
   documentation, the server returns the requested data as a `JSON
   <http://www.json.org/>`__ object. JSON objects are represented in
   Python as data structures made up of dictionaries, lists and
   strings. This makes JSON objects straightforward to manipulate from
   Python. The interface to the service is documented at
   https://environment.data.gov.uk/flood-monitoring/doc/reference.
