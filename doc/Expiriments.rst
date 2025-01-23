.. default-domain:: sphinxsharp



##################
Expiriments
##################
In the Nursing Simulation Experiments represent a collection of :ref:`Tasks` to be run in sequence.


.. _Tasks:

**************
Tasks
**************


Tasks serve as a way to unify all elements of your simulation into one managable unit.
The `Task.cs` abstract class provides the general structure of a Nursing Simulation task. 
Tasks contain information regaurding the task and its elements, as well as overidable functions for dictating the behavior of the task.
Most of the information needed for a task can be provided from the **inspector**. The below sections go over task information which can be provided via the inspector.

Task-related properties
----------------------

.. property:: public int IntProp { get; set; }

    Example of property with "get; set;" accessors.