Objects
###########

Objects provide both a way to make scenes more intresting, as well as probiding interactable obstacles and goals for tasks. 

Model Creation
***************

The first step in creating any kind of obstacle is building a model. Modeling is is a skillset that can take years to perfect, luckily, if manual modeling is not viable, there are alternate strategies for obtaining textured models.


Model Requirments
--------------------

Models must be imported in formats that are compatible with Unity. The most popular format being a **.obj** file with an acompanying material and texture image. Some formats use vertex coloring, this does not play well with unity and thus an extra step is required to convert to a useable format.


Premade Models
----------------

Many online vendors provide models either for free or for sale. One such vendor is Unit's own `Asset Store <https://assetstore.unity.com/>`_.


AI Generation
----------------

Currently AI model generation is in its infancy, however for simple models created from clear reference images, AI model generation can be viable. 

.. Could include sites but it is dificult to vet thier legitimacy

.. warning::
    Due to the controversial nature of AI art in relation to ownership, including AI generated content may have liscencing ramifications. Check IP laws before using this aproach.

Bespoke Modeling
------------------

Depending on user skill, simple models can be created from scratch using a program such as blender

.. Include learning materials here


File Conversion
****************

GLB Files
----------------

**.glb** is a common type for 3D models and textures to be backaged in. Unfortunatley without extensions Unity is unable to import these files directly. Below is a strategy for getting **.glb** files into the Nursing in Unity Simulation.


1. Open a new blender project and delete the default cube, light, and camera
2. Import the GLB file into your blender scene.

.. Note::
    At this point your mesh will likley apear untextured. This is expected. To verify your mesh has a texture switch your viewport shading to the **Material Preview** mode as shown below.
.. image:: images/shading.png
   :width: 400

3. Navigate to the **UV Editing** tab and select **Image > Save As**, save the texture as **<name>.png**
4. Select the model and navigate to **File > Export > Wavefront (.obj)**, make sure to export UVs and Normals, save the file as **<name>.obj**

At this point you can procede to :ref:`Model Importing`


Model Importing
****************

Obj Wavefront Files
---------------------



For this section we will asume you have the files:

- **<name>.obj**
- **<name>.png**

1. Navigate to **Assets > Import New Asset**
2. Select both files listed above and click import, both files should show in your asset viewer as below

.. image:: images/importedobj.png
   :width: 200

3. Select the model prefab and click the **Extract Masaterials** button in the **Inspector**.
4. When prompted select the folder you want to store the matieral (reccomended location is **assets > material > object**)
5. Rename the material to **<name>**
6. Move the imported texture (**name.png**) to the desired location (reccomended location is **assets > texture > object**)
7. Move the model prefab to the desired location (reccomended location is **assets > model > object**)
8. Finally select the imported material, select it, click the target icon next to **Base Map** as shown below, and select your texture

.. image:: images/basemap.png
   :width: 400

Your model is now fully imported and organized. At this point to turn it into a useable prefab see :ref:`Object Configuration`

Object Configuration
**********************

The first step when converting a model into a useable asset is creating a prefab. In the asset viewer navigate to the desired folder (reccomended location depends on function i.e. **assets > Prefabs > Interactable** or **assets > Prefabs > Object**) and create a new prefab.
Once the new prefab is created double click it to open the prefab in the editor. 

Model
---------

Drag your model into the **Game Object Hiearchy**. Multiple models can be used in one prefab if needed. It is reccomended to position models around the origin of the prefab.

Physics 
---------

Rigid Body
^^^^^^^^^^^

The first step in giving our prefab physics is to apply a rigid body. Select the model in the **Game Object Hiearchy** and add a new **Rigid Body** componant. Configure this as desired including adding gravity and mass propeties.

Next a collider is needed. Depending on the object primative coliders such as **Box Collider** and **Sphere Collider** compnants can be used to create a rough reepresentation of the object. 


Interaction
------------

Graspable
^^^^^^^^^^^
The **Graspable** script must be added to the prefab to allow for robots to properly grasp them

Auto Graspable
^^^^^^^^^^^^^^^
The **Auto Graspable** script must be added to the prefab to allow for robots to properly autonomously grasp them.
The script  has different properties including a **Grasp Point** this can be specified by creating an **Empty Game Object** in the prefab, and moving it to the desired grasp point.

XR Grab
^^^^^^^^

The XR Grab Interactable componant can be applied to make the object manipulatable for XR users such as a VR Nurse.



