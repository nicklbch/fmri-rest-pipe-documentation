Requirements
=====


Docker Dependencies
------------

The following docker images must be available and added to the environment 

● sms-mi-reg Docker Container: https://github.com/ComputationalRadiology/sms-mi-reg/

*motion-monitor Docker Container: https://github.com/josh-auger/motion-monitor

*heudiconv Docker Container: https://hub.docker.com/r/nipy/heudiconv

-fmriprep Docker Container: https://hub.docker.com/r/nipreps/fmriprep

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']


