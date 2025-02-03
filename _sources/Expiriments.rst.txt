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
Tasks can be run individually via the `RunTask.cs` script.

Task-related properties
---------------------------


.. variable:: public  string TaskName

   Name of this task

.. variable:: public  string TaskDescription 

   Description of this task. *(Displayed on GUI)*

Scene Setup
^^^^^^^^^^^
.. variable:: public  string SceneName 

   Name of scene to use for task. Ex. **Hospital**. 

.. important::
   Spawning of robots, static objects, dynamic objects, task objects, and goal objects, are all handled by :ref:`Tasks`. This means your Scene **should not** include these objects.

Spawnables
^^^^^^^^^^^

Spawnables represent **GameObjects** whos spawning behavior is handled by :ref:`Tasks`. This includes the Robot, goals, and all static and dynamic task objects.
Spawnables are created in the **Inspector** using the **Spawn Info** struct.

SpawnInfo 
""""""""""""""
.. type:: public  struct SpawnInfo

    This type is now a parent for it childrens.

.. variable:: public  GameObject gameObject

    **GameObject** to be spawned (given as prefab)

.. variable:: public  Vector3 position

    Position to spawn object at.

.. variable:: public  Vector3 rotation

    Rotation to spawn object wtih.

.. variable:: public  Vector3[] trajectory

    Trajectory to spawn target object with given as waypoints


.. end-type::

.. raw:: html

   <hr>

.. variable:: public  SpawnInfo[] StaticObjectSpawnArray

   Array of static objects to be spawned. Used for things like unmovable obsticles.

.. variable:: public  SpawnInfo[] DynamicObjectSpawnArray

   Array of dynamic objects to be spawned. Dynamic objects are expected to have a **CharacterNavigation** componant.

.. variable:: public  SpawnInfo[] TaskObjectSpawnArray

   Array of task related objects to be spawned

.. variable:: public  SpawnInfo[] GoalObjectSpawnArray
2
   Array of goal objects to be spawned. Goal objects are expected to have a **Goal** componant.

Robot
^^^^^^^^^^^

.. variable:: public  SpawnInfo[] robotSpawnArray

   Array of static robots to be spawned

.. important::
   The GUI will only be linked to the robot at **index 0** of :var:`robotSpawnArray`

Interface
^^^^^^^^^^^

.. variable:: public  GraphicalInterface GoalObjectSpawnArray

   Graphical interface to be used in this task


.. variable:: public  ControlInterface GoalObjectSpawnArray

   Control interface to be used in this task


Task-related functions
---------------------------

By overriding the following functions different task procedures can be implimented.

Task Status Functions
^^^^^^^^^^^^^^^^^^^^^^

.. method:: public  virtual bool CheckTaskStart()
   
   The default behavior of this function is to return **False** if no robot is present, or if the robot has not deviated more than 0.1m from the starting position, and **True** otherwise.
   
   :returns: **True** if task has started, **False** otherwise

.. method:: public  virtual float GetTaskDuration()
   
   The default behavior of this function is to return **0** if the task has not started and the current ellapsed time of the task otherwise.
   
   :returns: Current ellapsed time of task as a **Float**

.. method:: public  virtual bool CheckTaskCompletion()

   The default behavior of this function is to return **False** until a 10 minute timer has run out at which point it returns **True**
   
   :returns: **False** if task is in progress or **True** if task has completed.

.. method:: public  virtual string SetResult()

   Responsible for providing a human readable task status to the GUI

   The default behavior of this function is to return an empty string.
   
   :returns: Human readable task status string.

.. method:: public  virtual void CheckInput(string input)
   :param(1): User input given from GUI

   This function can be used for processing user input provided in the GUI. Ex. having users complete a secondary math task and proccessin thier answers.

   The default behavior of this function is to store the input in the **userInput** variable and set the **userInputRecived** flag to **True**

.. method:: public  virtual string ResetTask()

   Used when a task needs to be reloaded.

   The default behavior of this function is to set the **taskStarted** flag to false.




Object Generation Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. method:: public  virtual GameObject[] GenerateStaticObjects()
   
   This function is responsible for initializing :var:`StaticObjectSpawnArray` and making sure each initialized object is in the state it should be at the start of the task.

   The default behavior of this function is to spawn all items in :var:`StaticObjectSpawnArray` and store them in the **staticObjects** variable.
   :returns: Array of spawned GameObjects


.. warning::
   When overriding Generate functions it is imparative to first call the super method. If you wish to only spawn some ojects, the reccomended way to do so is call the super method, and then iterate over the generated GameObjects and use the **setActive** function to disable any objects you dont wish to be present.


.. method:: public  virtual GameObject[] GenerateDynamicObjects()
   
   This function is responsible for initializing :var:`DynamicObjectSpawnArray` and making sure each initialized object is in the state it should be at the start of the task.

   The default behavior of this function is to spawn all items in :var:`DynamicObjectSpawnArray` and store them in the **dynamicObjects** variable.
   As well as spawning the objects, this method populates each objects **CharacterNavigation** componant with the trajectory given by thier respective :type:`SpawnInfo` trajectory.
   
   :returns: Array of spawned GameObjects

.. method:: public  virtual GameObject[] GenerateTaskObjects()
   
   This function is responsible for initializing :var:`TaskcObjectSpawnArray` and making sure each initialized object is in the state it should be at the start of the task.

   The default behavior of this function is to spawn all items in :var:`TaskcObjectSpawnArray` and store them in the **taskObjects** variable.
   
   :returns: Array of spawned GameObjects

.. method:: public  virtual GameObject[] GenerateGoalObjects()
   
   This function is responsible for initializing :var:`GoalObjectSpawnArray` and making sure each initialized object is in the state it should be at the start of the task.

   The default behavior of this function is to spawn all items in :var:`GoalObjectSpawnArray` and store them in the **goalObjects** variable.
   As well as spawning the objects, this method populates the **goals** variable with the **Goal** componants of each spawned object.

   :returns: Array of spawned GameObjects


.. method:: public  virtual GameObject[] GenerateRobots()
   
   This function is responsible for initializing :var:`robotSpawnArray` and making sure each initialized object is in the state it should be at the start of the task.

   The default behavior of this function is to spawn all items in :var:`robotSpawnArray` and store them in the **robots** variable.
   As well as spawning robots this method is also responsible for linking the GUI to the first robot as well as the current task.
   :returns: Array of spawned GameObjects