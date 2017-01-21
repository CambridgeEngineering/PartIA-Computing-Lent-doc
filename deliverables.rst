.. _Deliverables:

Deliverables
============

This section describes the project deliverables.  Functionality is to
be implemented in the the module ``floodsystem``.

.. rubric:: Milestones and deadlines

Project deliverables/tasks are structured into two milestones.
Milestone 1 must be delivered by the mid-term marking session, and
Milestone 2 by the end-of-term marking session.  You may deliver early
by signing off at a support session.

.. rubric:: Task completion, interfaces and demonstration programs

Each task requires the implementation of specified functionality that
can be accessed via a specified interface, usually a function
signature (function name and arguments, and return values).  At the
end of each task is a description of a demonstration program that must
be be provided. Demonstration programs must have the structure::

  def run():
      # Put code here that demonstrates functionality

  if __name__ == "__main__":
      run()

You should expect to run demonstration programs during a marking
session.


.. rubric:: Testing

Write tests as you progress through the tasks (see
:ref:`using-pytest`).


.. tip::

   To deliver on a Task, you will often want to implement more
   functions than just the required function interface. Use additional
   functions to:

   - Modularise and simplify your library.
   - Allow re-use of functions across tasks.
   - Simplify testing.

   As you work through the Tasks, look for opportunities to
   re-structure code in order to re-use functions.

.. important::

   Conforming to the specified public interface is critical as this
   will allow the interface team to work independently of your
   development (and it will allow automated testing of your work).

.. topic:: Units

   Distances in kilometres (km) and heights in metres (m).

Milestone 1
-----------

Processing of monitoring station properties.

:Deadline: Mid-term sign-up session
:Points: 4

.. warning::

   Do not use the 'representative output' in your pytest tests.
   'Representative output' is provided to help you, but would not be
   part of a real contract. Moreover, you are working with realtime
   data which is subject to change.


Task 1A: build monitoring station data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*This task has been completed for you in the template repository.*

In a submodule ``station``, create a class ``MonitoringStation`` that
represents a monitoring station, and has *attributes*:

- Station ID (``string``)
- Measurement ID (``string``)
- Name (``string``)
- Geographic coordinate (``tuple(float, float)``)
- Typical low/high levels (``tuple(float, float)``)
- River on which the station is located (``string``)
- Closest town to the station (``string``)

Also, implement the *methods* ``__init__`` to initialise a station
with data, and ``__repr__`` for printing a description of the station.

In the submodule ``stationdata`` implement a function that returns a
`list <https://docs.python.org/3/library/stdtypes.html#lists>`_ of
``MonitoringStation`` objects (for active stations with water level
monitoring).  To avoid excessive data requests, the function should
save fetched data to file, and then optionally read from a cache file.
The function should have the signature::

  def build_station_list(use_cache=True):

The data should be retrieved from the online service documented at
http://environment.data.gov.uk/flood-monitoring/doc/reference.

.. topic:: Demonstration program

   In the program file ``Task1A.py``, use the function
   ``stationdata.build_station_list`` to build a list of monitoring
   stations. Print the total number of stations, and a summary of the
   stations named 'Bourton Dickler', 'Surfleet Sluice' and 'Gaw
   Bridge'. Representative output is:

   .. code-block:: none

      Number of stations: 1840
      Station name:     Bourton Dickler
         id:            http://environment.data.gov.uk/flood-monitoring/id/stations/1029TH
         measure id:    http://environment.data.gov.uk/flood-monitoring/id/measures/1029TH-level-stage-i-15_min-mASD
         coordinate:    (51.874767, -1.740083)
         town:          Little Rissington
         river:         Dikler
         typical range: (0.068, 0.42)
      Station name:     Surfleet Sluice
         id:            http://environment.data.gov.uk/flood-monitoring/id/stations/E2043
         measure id:    http://environment.data.gov.uk/flood-monitoring/id/measures/E2043-level-stage-i-15_min-mASD
         coordinate:    (52.845991, -0.100848)
         town:          Surfleet Seas End
         river:         River Glen
         typical range: (0.15, 0.895)
      Station name:     Gaw Bridge
         id:            http://environment.data.gov.uk/flood-monitoring/id/stations/52119
         measure id:    http://environment.data.gov.uk/flood-monitoring/id/measures/52119-level-stage-i-15_min-mASD
         coordinate:    (50.976043, -2.793549)
         town:          Kingsbury Episcopi
         river:         River Parrett
         typical range: (0.231, 0.971)


Task 1B: sort stations by distance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the submodule ``geo`` implement a function that, given a list of
stations and a coordinate *p*, returns a `list
<https://docs.python.org/3/library/stdtypes.html#lists>`__ of
``(station, distance)`` `tuples
<https://docs.python.org/3/library/stdtypes.html#tuples>`__, where
``distance`` (``float``) is the distance of the ``station``
(``MonitoringStation``) from the coordinate *p*.  The returned list
should be sorted by distance. The required function signature is::

  def stations_by_distance(stations, p):

where ``stations`` is a list of ``MonitoringStation`` objects and
``p`` is a tuple of floats for the coordinate *p*.

.. tip::

   Distances between two geographic coordinates (latitude/longitude)
   are computed using the `haversine formula
   <https://en.wikipedia.org/wiki/Haversine_formula>`__. You could
   program the haversine formula, or you could use a Python library to
   perform the computation for you,
   e.g. https://github.com/mapado/haversine.

.. hint::

   Build a list of all ``(station, distance)`` tuples, and use the
   provided function ``utils.sort_by_key`` to produce a list that is
   sorted by the second entry in the tuple.

.. topic:: Demonstration program

   Provide a program file ``Task1B.py`` that uses
   ``geo.stations_by_distance`` and prints a list of tuples (station
   name, town, distance) for the 10 closest and the 10 furthest stations
   from the Cambridge city centre, (52.2053, 0.1218).  The closest 10
   entries (e.g., ``x[:10]``) in the list should be:

   .. code-block:: none

      [('Cambridge Jesus Lock', 'Cambridge', 0.8402364350834995), ('Bin Brook', 'Cambridge', 2.502274086951454), ("Cambridge Byron's Pool", 'Grantchester', 4.0720438555077125), ('Cambridge Baits Bite', 'Milton', 5.115589516578674), ('Girton', 'Girton', 5.227070345811418), ('Haslingfield Burnt Mill', 'Haslingfield', 7.044388165868453), ('Oakington', 'Oakington', 7.128249171700346), ('Stapleford', 'Stapleford', 7.265694306995238), ('Comberton', 'Comberton', 7.7350743760373675), ('Dernford', 'Great Shelford', 7.993861351711722)]

   and the furthest 10 (e.g., ``x[-10:]``):

   .. code-block:: none

      [('Boscadjack', 'Wendron', 440.0026482838576), ('Gwithian', 'Gwithian', 442.05491558132354), ('Helston County Bridge', 'Helston', 443.37824966454974), ('Loe Pool', 'Helston', 445.07184458260684), ('Relubbus', 'Relubbus', 448.64944322554413), ('St Erth', 'St Erth', 449.03415711886015), ('St Ives Consols Farm', 'St Ives', 450.0734690482922), ('Penzance Tesco', 'Penzance', 456.3857579793324), ('Penzance Alverton', 'Penzance', 458.5766422710278), ('Penberth', 'Penberth', 467.53367291629183)]


Task 1C: stations within radius
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the submodule ``geo`` implement a function that returns a `list
<https://docs.python.org/3/library/stdtypes.html#lists>`__ of all
stations (type ``MonitoringStation``) within radius *r* of a
geographic coordinate *x*. The required function signature is::

  def stations_within_radius(stations, centre, r):

where ``stations`` is a list of ``MonitoringStation`` objects,
``centre`` is the coordinate *x* and ``r`` is the radius.

.. topic:: Demonstration program

   Provide a program file ``Task1C.py`` that uses the function
   ``geo.stations_within_radius`` to build a list of stations within
   10 km of the Cambridge city centre (coordinate (52.2053,
   0.1218)). Print the names of the stations, listed in alphabetical
   order. A representative result is:

   .. code-block:: none

      ['Bin Brook', 'Cambridge Baits Bite', "Cambridge Byron's Pool",
       'Cambridge Jesus Lock', 'Comberton', 'Dernford', 'Girton',
       'Haslingfield Burnt Mill', 'Lode', 'Oakington', 'Stapleford']


Task 1D: rivers with a station(s)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the submodule ``geo`` develop a function that, given a list of
stations, returns all rivers (by name) with a monitoring station. The
function should have the signature::

  def rivers_with_station(stations):

.. tip::

   Return a Python `set
   <https://docs.python.org/3/library/stdtypes.html#set>`__ object. A
   set contains only unique elements. This is useful for building a
   collection of river names since a set will never contain duplicate
   entries, no matter how many times a river name is added.  A brief
   example of using a ``set`` is available `here
   <https://docs.python.org/3/tutorial/datastructures.html#sets>`__.

In the submodule ``geo`` implement a function that returns a Python
``dict`` (dictionary) that maps river names (the 'key') to a list of
stations on a given river. The function should have the signature::

  def stations_by_river(stations):

.. topic:: Demonstration program

   Provide a program file ``Task1D.py`` that:

   - Uses ``geo.rivers_with_station`` to print how many rivers
     have at least one monitoring station (Representative result: 843)
     and prints the first 10 of these rivers in alphabetical order.
     Representative result:

     .. code-block:: none

        ['Addlestone Bourne', 'Adur', 'Aire Washlands', 'Alconbury Brook',
         'Aldbourne', 'Aller Brook', 'Alre', 'Alt', 'Alverthorpe Beck', 'Ampney Brook']

   - Uses ``geo.stations_by_river`` to print the names of the
     stations located on the following rivers in alphabetical order:

     - 'River Aire'

       Representative result:

       .. code-block:: none

          ['Airmyn', 'Apperley Bridge', 'Armley', 'Beal Weir Bridge', 'Bingley', 'Birkin Holme Washlands', 'Carlton Bridge', 'Castleford', 'Chapel Haddlesey', 'Cononley', 'Cottingley Bridge', 'Ferrybridge Lock', 'Fleet Weir', 'Gargrave', 'Kildwick', 'Kirkstall Abbey', 'Knottingley Lock', 'Leeds Crown Point', 'Saltaire', 'Snaygill', 'Stockbridge']

     - 'River Cam'

       Representative result:

       .. code-block:: none

          ['Cam', 'Cambridge', 'Cambridge Baits Bite', 'Cambridge Jesus Lock', 'Dernford', 'Weston Bampfylde']

     - 'Thames'

       Representative result:

       .. code-block:: none

          ['Abingdon Lock', 'Bell Weir', 'Benson Lock', 'Boulters Lock', 'Bray Lock', 'Buscot Lock', 'Caversham Lock', 'Chertsey Lock', 'Cleeve Lock', 'Clifton Lock', 'Cookham Lock', 'Cricklade', 'Culham Lock', 'Days Lock', 'Ewen', 'Eynsham Lock', 'Farmoor', 'Godstow Lock', 'Goring Lock', 'Grafton Lock', 'Hannington Bridge', 'Hurley Lock', 'Iffley Lock', 'Kings Lock', 'Kingston', 'Maidenhead', 'Mapledurham Lock', 'Marlow Lock', 'Marsh Lock', 'Molesey Lock', 'Northmoor Lock', 'Old Windsor Lock', 'Osney Lock', 'Penton Hook', 'Pinkhill Lock', 'Radcot Lock', 'Reading', 'Romney Lock', 'Rushey Lock', 'Sandford-on-Thames', 'Shepperton Lock', 'Shifford Lock', 'Shiplake Lock', 'Somerford Keynes', 'Sonning Lock', 'St Johns Lock', 'Staines', 'Sunbury  Lock', 'Sutton Courtenay', 'Teddington Lock', 'Thames Ditton Island', 'Trowlock Island', 'Walton', 'Whitchurch Lock', 'Windsor Park']


Task 1E: rivers by number of stations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Implement a function in ``geo`` that determines the *N* rivers with
the greatest number of monitoring stations. It should return a list of
(river name, number of stations) tuples, sorted by the number of
stations.  In the case that there are more rivers with the same number
of stations as the *N* th entry, include these rivers in the list. The
function should have the signature::

  def rivers_by_station_number(stations, N):

.. topic:: Demonstration program

   Provide a program file ``Task1E.py`` that prints the list of
   (number stations, river) tuples when *N* = 9. Representative result
   is:

   .. code-block:: none

      [('Thames', 55), ('River Great Ouse', 31), ('River Avon', 30), ('River Calder', 24), ('River Aire', 21), ('River Severn', 20), ('River Derwent', 18), ('River Stour', 16), ('River Wharfe', 14), ('River Trent', 14), ('Witham', 14)]

   Note that this list has more then 9 entries since a number of
   rivers have 14 stations.


Task 1F: typical low/high range consistency
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It is suspected that some stations have inconsistent data for typical
low/high ranges, namely that no data is available or the reported
typical high range is less than the reported typical low. This needs
to be checked so that stations with inconsistent data are not used
erroneously in flood warning analysis.

Add a *method* to the ``MonitoringStation`` class that checks the
typical high/low range data for consistency.  The method should return ``True``
if the data is consistent and ``False`` if the data is inconsistent or
unavailable.  The method should have the signature::

  def typical_range_consistent(self):

Implement in the submodule ``station`` a function that, given a list of
stations objects, returns a list of stations that have inconsistent
data. The function should use
``MonitoringStation.typical_range_consistent``, and should have the
signature::

  def inconsistent_typical_range_stations(stations):

.. topic:: Demonstration program

   Provide a program file ``Task1F.py`` that builds a list of all
   stations with inconsistent typical range data.  Print a list of
   stations names, in alphabetical order, for stations with
   inconsistent data. The representative result (at the time of
   writing) is:

   .. code-block:: none

      ['Addlestone', 'Airmyn', 'Allerford', 'Arundel Queen St Bridge', 'Blacktoft', 'Braunton', 'Brentford', 'Broomfleet Weighton Lock', 'East Hull Hedon Road', 'Eccelsfield Morrisons', 'Fleetwood', 'Goole', 'Gravesend', 'Hedon Thorn Road Bridge', 'Hedon Westlands Drain', 'Hull Barrier Victoria Pier', 'Hull High Flaggs, Lincoln Street', "King's Lynn", 'Littlehampton', 'Paull', 'Salt end', 'Silloth Docks', 'Stone Creek', 'Templers Road', 'Topsham', 'Totnes', 'Truro Harbour', 'Weare Giffard', 'Westbrook Mill', 'Wilfholme PS', 'Wilfholme PS Hull Level']


Optional extensions
^^^^^^^^^^^^^^^^^^^

- Display the location of each station on a map (perhaps from Google
  Maps).  Suitable Python libraries tools for this include `Bokeh
  <http://bokeh.pydata.org/>`__ and `Plotly
  <https://plot.ly/python/#maps>`__.

- Explore what other station information is available in the retrieved
  data. The function ``stationdata.build_station_list`` is a good
  place to start. Extend ``MonitoringStation`` to store any
  interesting station data as attributes.

- *Advanced*: The ``MonitoringStation`` attributes (station data) are
  properties of the station and will not generally change. However, we
  could accidentally and mistakenly change an attribute in our
  code. For flood forecasting and warning, such an error could have
  dire consequences.  Use `property
  <https://docs.python.org/3/library/functions.html#property>`__
  decorators to prevent accidental modification of the attributes.

.. todo::

   Add example code for using Bokeh with Google Maps.


Milestone 2
-----------

The focus of the Milestone 2 is processing monitoring station
real-time data to warn of flood risks.

:Deadline: End-of-term sign-up session
:Points: 8

.. caution::

   Representative output for each demonstration program is provided as
   a guide. You will be working with real-time data, so the precise
   output will change with time.


Task 2A: fetch real-time river levels
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*This task has been completed for you in the template repository.*

Extend the ``MonitoringStation`` class with an attribute
``latest_level`` (``float``), and implement in the ``stationdata``
submodule a function that updates the latest water level for all
stations in a list using data fetched from the Internet.  If level
data is not available, the attribute ``latest_level`` should be set to
``None``. The function should have the signature::

  def update_water_levels(stations):

.. topic:: Demonstration program

   Provide a program file ``Task2A.py`` that sets the latest water
   level for all stations, and prints the latest levels at the
   stations 'Bourton Dickler', 'Surfleet Sluice', 'Gaw Bridge',
   'Hemingford' and 'Swindon'. Typical output is:

   .. code-block:: none

      Station name and current level: Bourton Dickler, 0.146
      Station name and current level: Surfleet Sluice, 0.84
      Station name and current level: Gaw Bridge, 0.463
      Station name and current level: Hemingford, 0.197
      Station name and current level: Swindon, 1.192


Task 2B: assess flood risk by level
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add a method to ``MonitoringStation`` that the returns the latest
water level as a fraction of the typical range, i.e. a ratio of 1.0
corresponds to a level at the typical high and a ratio of 0.0
corresponds to a level at the typical low. The method should have the
signature::

  def relative_water_level(self):

If the necessary data is not available or is inconsistent, the
function should return ``None``.

In the submodule ``flood``, implement a function that returns a list
of tuples, where each tuple holds (1) a station at which the latest
relative water level is over ``tol`` and (2) the relative water level
at the station. The returned list should be sorted by the relative
level in descending order. The function should have the signature::

  def stations_level_over_threshold(stations, tol):

Consider only stations with consistent typical low/high data.

.. topic:: Demonstration program

   Provide a program file ``Task2B.py`` that prints the name of each
   station at which the current relative level is over 0.8, with the
   relative level alongside the name (do not forget to handle the
   cases of inconsistent range data). Typical output will be of the
   form:

   .. code-block:: none

      Ledgard Bridge 3.982
      Godstow Lock 1.56198347107438
      Windyridge Road 1.4470588235294117
      Castle Mill (Bedford) 1.3333333333333328
      Newark Weir 1.249999999999988
      Cam 1.1813725490196074
      Hayes Basin 1.166666666666667
      Eckington Sluice 1.0875462392108504
      Romney Lock 1.0829268292682928
      Pinkhill Lock 1.0524475524475525
      .
      .

   Explore your implementation for different tolerances.


Task 2C: most at risk stations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Implement a function in the submodule ``flood`` that returns a list of
the *N* stations at which the water level, relative to the typical
range, is highest. The list should be sorted in descending order by
relative level.  The function should have the signature::

  def stations_highest_rel_level(stations, N):

.. topic:: Demonstration program

   Provide a program file ``Task2C.py`` that prints the names of the
   10 stations at which the current relative level is highest, with
   the relative level beside each station name.  Typical output will
   be of the form:

   .. code-block:: none

      Ledgard Bridge 3.982
      Godstow Lock 1.56198347107438
      Windyridge Road 1.4470588235294117
      Castle Mill (Bedford) 1.3333333333333328
      Newark Weir 1.249999999999988
      Cam 1.1813725490196074
      Hayes Basin 1.166666666666667
      Eckington Sluice 1.0875462392108504
      Romney Lock 1.0829268292682928
      Pinkhill Lock 1.0524475524475525


Task 2D: level data time history
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*This task has been completed for you in the template repository.*

Implement in the submodule ``datafetcher`` a function that retrieves
from the Internet the water level data for a given station 'measure
id' over the period from the current time back to *d* days ago. It
should return a tuple with the first entry being the sample times and
the second entry being the water levels.  The function should have the
signature::

  def fetch_measure_levels(measure_id, dt):

Typical use to retrieve the level data at a station over the past 10
days would be::

  import datetime
  dt = 10
  dates, levels = fetch_measure_levels(station.measure_id,
                                       dt=datetime.timedelta(days=dt))

.. topic:: Demonstration program

   Provide a program file ``Task2D.py`` that fetches and prints the
   level history at the station 'Cam' over the past 2 days. Typical
   output:

   .. code-block:: none

      2017-01-08 04:00:00+00:00 0.819
      2017-01-08 03:45:00+00:00 0.819
      2017-01-08 03:30:00+00:00 0.819
      2017-01-08 03:15:00+00:00 0.819
      2017-01-08 03:00:00+00:00 0.819
      2017-01-08 02:45:00+00:00 0.819
      2017-01-08 02:30:00+00:00 0.819
      2017-01-08 02:15:00+00:00 0.819
      2017-01-08 02:00:00+00:00 0.82
      2017-01-08 01:45:00+00:00 0.82
      .
      .


Task 2E: plot water level
^^^^^^^^^^^^^^^^^^^^^^^^^

Implement in a submodule ``plot`` a function that displays a plot
(using `Matplotlib <http://matplotlib.org/>`__) of the water level
data against time for a station, and include on the plot lines for the
typical low and high levels. The axes should be labelled and use the
station name as the plot title. The function should have the
signature::

  def plot_water_levels(station, dates, levels):

*Option:* In place of Matplotlib, try using a web-centric Python
plotting library such as `Bokeh <http://bokeh.pydata.org/>`__ or
`Plotly <https://plot.ly/python/>`__.

*Optional extension:* Generalise your implementation such that it
takes a list of up to 6 stations displays the level at each station as
subplot inside a single plot.

.. todo::

   Add subplot example or link

.. hint::

   Example code to display a plot using Matplotlib::

     import matplotlib.pyplot as plt
     from datetime import datetime, timedelta

     t = [datetime(2016, 12, 30), datetime(2016, 12, 31), datetime(2017, 1, 1),
          datetime(2017, 1, 2), datetime(2017, 1, 3), datetime(2017, 1, 4),
          datetime(2017, 1, 5)]
     level = [0.2, 0.7, 0.95, 0.92, 1.02, 0.91, 0.64]

     # Plot
     plt.plot(t, level)

     # Add axis labels, rotate date labels and add plot title
     plt.xlabel('date')
     plt.ylabel('water level (m)')
     plt.xticks(rotation=45);
     plt.title("Station A")

     # Display plot
     plt.tight_layout()  # This makes sure plot does not cut off date labels
     plt.show()

.. topic:: Demonstration program

   Provide a program file ``Task2E.py`` that plots the water levels
   over the past 10 days for the 5 stations at which the current
   relative water level is greatest.

   *Optional extension:* Generalise your implementation such that it
   takes a list of up to 6 stations displays the level versus time for
   each station as subplot inside a single plot.


Task 2F: function fitting
^^^^^^^^^^^^^^^^^^^^^^^^^

.. sidebar:: Least-squares polynomial fit

   A least-squares polynomial fit is finding a polynomial that 'best'
   fits data points in the least-squares sense, i.e.  for a set of
   :math:`n` data points

   .. math::

      ((x_0, y_0), (x_1, y_1), \dots, (x_{n-1}, y_{n-1}))

   the best-fit polynomial :math:`f(x)` minimises the error

   .. math::

      e = \sum_{i=0}^{n-1} (y_{i} - f(x_{i}))^{2}.

   Details of how to compute least-squares fits is covered in Part IB.

In a submodule ``analysis`` implement a function that given the water
level time history (dates, levels) for a station computes a
least-squares fit of polynomial of degree *p* to water level data.
The function should return a tuple of (1) the polynomial object
and (2) any shift of the time (date) axis (see below).  The function
should have the signature::

  def polyfit(dates, levels, p):

Typical usage for a polynomial of degree 3 would be::

  poly, d0 = polyfit(dates, levels, 3)

where ``poly`` is a `numpy.poly1d
<https://docs.scipy.org/doc/numpy/reference/generated/numpy.poly1d.html>`__
object an ``d0`` is any shift of the date (time) axis.

.. hint::

   To work with dates as function arguments, e.g. a polynomial that
   depends on time, the dates need to be converted to
   floats. Matplotlib has a function that from a list of ``datetime``
   objects returns a list of ``float``, where the floats are the time
   in days since the year 0001::

     import matplotlib
     x = matplotlib.dates.date2num(dates)

.. hint::

   NumPy has tools for computing least-squares fits to data. The below
   example computes a least-squares fit for some data points, and
   plots the data points and the least-squares polynomial::

     import numpy as np
     import matplotlib.pyplot as plt

     # Create set of 10 data points on interval (0, 2)
     x = np.linspace(0, 2, 10)
     y = [0.1, 0.09, 0.23, 0.34, 0.78, 0.74, 0.43, 0.31, 0.01, -0.05]

     # Find coefficients of best-fit polynomial f(x) of degree 4
     p_coeff = np.polyfit(x, y, 4)

     # Convert coefficient into a polynomial that can be evaluated,
     # e.g. poly(0.3)
     poly = np.poly1d(p_coeff)

     # Plot original data points
     plt.plot(x, y, '.')

     # Plot polynomial fit at 30 points along interval
     x1 = np.linspace(x[0], x[-1], 30)
     plt.plot(x1, poly(x1))

     # Display plot
     plt.show()

.. caution::

   In the above example, if we changed the ``x`` interval (0, 2) to
   (10000, 10002), i.e.::

     x = np.linspace(10000, 10002, 10)

   NumPy prints the warning message::

     RankWarning: Polyfit may be poorly conditioned warnings.warn(msg, RankWarning)

   This message is warning that floating point round-off errors will
   be significant and will affect accuracy. In simple terms, the
   issues is that when we raise a number between 10000 and 10002 to a
   power, small but important differences are effectively 'lost'.

   This issues arises if we work with dates converted to floats using
   ``matplotlib.dates.date2num`` since it returns the number of days
   since the origin of the Gregorian calendar. The numbers will
   therefore be large.  A way to improve the situation is with a
   change-of-variable::

     import numpy as np
     import matplotlib.pyplot as plt

     # Create set of 10 data points on interval (1000, 1002)
     x = np.linspace(10000, 10002, 10)
     y = [0.1, 0.09, 0.23, 0.34, 0.78, 0.74, 0.43, 0.31, 0.01, -0.05]

     # Using shifted x values, find coefficient of best-fit
     # polynomial f(x) of degree 4
     p_coeff = np.polyfit(x - x[0], y, 4)

     # Convert coefficient into a polynomial that can be evaluated
     # e.g. poly(0.3)
     poly = np.poly1d(p_coeff)

     # Plot original data points
     plt.plot(x, y, '.')

     # Plot polynomial fit at 30 points along interval (note that polynomial
     # is evaluated using the shift x)
     x1 = np.linspace(x[0], x[-1], 30)
     plt.plot(x1, poly(x1 - x[0]))

     # Display plot
     plt.show()

In the submodule ``plot``, add a function that plots the water level
data and the best-fit polynomial. The function must have the
signature::

  def plot_water_level_with_fit(station, dates, levels, p):

.. topic:: Demonstration program

   Provide a program file ``Task2F.py`` that for each of the 5 stations at
   which the current relative water level is greatest and for a time
   period extending back 2 days, plots the level data and the best-fit
   polynomial of degree 4 against time. Show the typical range
   low/high on your plot.

.. caution::

   Fitting high-degree polynomials to data is notoriously tricky,
   especially if the data is not very smooth (as will often be the
   case with water level data). The problem is that oscillations can
   appear at the ends of the interval. The is known as `Runge's
   phenomenon <https://en.wikipedia.org/wiki/Runge's_phenomenon>`__.
   You can observe this with the river level data by increasing the
   polynomial degree, say to 10, and the time interval, say to 10
   days.


Task 2G: issuing flood warnings for towns
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using your implementation, list the towns where you assess the risk of
flooding to be greatest. Explain the criteria that you have used in
making your assessment, and rate the risk at 'severe', 'high',
'moderate' or 'low'.

.. note::

   The task is an opportunity to demonstrate your creativity and
   technical insights.

.. tip::

   Consider how you could forecast whether the water level at a
   station is rising or falling.


Optional extensions
^^^^^^^^^^^^^^^^^^^

- Show all stations on a map, and indicate by colour stations that
  are (i) below the typical range; (ii) within the typical range;
  (iii) above the typical range; or (iv) for which there is not level
  data.

- Provide a web-based interface to your flood warning system.

- Explore what extra data from
  http://environment.data.gov.uk/flood-monitoring/doc/reference you
  could use to improve your monitoring and warning system.  To start,
  examine the data that is already being retrieved but has not been
  used.
