## Key Dates
**Assigned:** TBD
**Due:** TBD
**Help Sessions:** TBD

![](https://courses.cs.washington.edu/courses/cse457/21wi/img/modeler/modeler_logo.jpg)
## Overview
### Description
Modeler is a 3D modelling program that lets you design and edit 3D scenes, similar to tools such as Maya, 3DS Max, and Blender. In Modeler, you can set up and arrange 3D elements in a scene, which serves as a stepping stone where you will extend this program to animate your scene.

The two requirements in this program include geometric modelling (specifying the basic 3D shapes of objects in the scene) and hierarchial scene modelling (specifying the relative arrangement of objects in the scene).

-   **Geometric Modelling**: Constructing Surfaces of Revolution
-   **Hierarchical Modeling**: Creating a hierarchical model that has at least 2 levels of branching and animating 2 animations 

### Getting Started
- Download and get familiar with the Sample Solution to see how everything works, especially the construction of Surfaces of Revolution.

## Requirements

Implement the features described below. The skeleton code has comments marked with  `// REQUIREMENT`  denoting the locations at which you probably want to add some code.

-   #### Surface of Revolution
    
    Write code to create a 3D surface of revolution mesh in the  **SurfaceOfRevolution::CreateMesh**  method in  **scene/components/surfaceofrevolution.cs**. Your shape must:
    
    -   have appropriate positions for each vertex
        
    -   have appropriate per-vertex normals
        
    -   have appropriate texture coordinates for each vertex
        
    -   have appropriate vertex connectivity (triangle faces)
        
    -   use the "subdivisions" argument to determine how many bands your surface is sliced into.
    
- #### Hierarchical Modeling
    
    Your artifact for this assignment will involve creating a hierarchical model. This model must have at least two levels of branching.
    
    There are two parts to this requirement:
    
    -   This model must have at least two levels of branching.
    -  In Play Mode, this model must automatically demonstrate two animations which we give more details about below.
    
    We recommend you refer to class lectures and write down the tree diagram of your model to help you figure out what your model will be, and to practice thinking about empty nodes, centers of rotation, and so on. But note the tree diagram is not a requirement.
    
    The second requirement gives you a chance to model some dynamically animated actions which act as a stepping stone to your last projects.
    
  

## Program Usage (not quite done, need to integrate Hierarchical Model into the Modeler repo)


The  **Hierarchy**  tab in the left pane represents all the objects in the current Scene. A child object inherits the transformations applied to the parent object like in a scene graph. Parent-Child relationships can changed by simply dragging the objects around in the pane. You may also find creating Empty objects as parents to be useful in building your model. 


The  **Assets**  tab in the left pane represents things like Textures, Shaders, Materials, and Meshes used by the Scene. Materials use Shaders, and shaders use .vert and .frag files. You can either edit them in the right-side Inspector, or choose to create a new asset. Together, the Assets and Scene Graph form a "Scene", and can be saved out or loaded from disk.

  
Selecting an asset or an object will display their properties on the right side in the Inspector. Here you can change their properties, assign different textures, materials, etc. For scene objects, you can also hide them from the hierarchy by unchecking the box by their name on the **Inspector** tab.

Modeler uses a component based system for scene objects. Every object has a "Transform" component that represents their Position, Rotation, and Scale in 3D space. From the **Inspector** tab, most rendered objects will have a "Mesh Filter" that takes a mesh passes it into a "Mesh Renderer" that uses a "Material" asset to define how to render that shape. Lights will have an additional "Light" component that defines the light properties.

The **Console** tab  at the bottom is mostly for debugging purposes, at any time in your code, you can call  _Debug.Log("...")_  to print to this console. If you hide the Inspector or any of the other panels in the program, right-click on the tool-bar to show them again.

## Skeleton Program (not done, needs full integration in project)
For the most part, you will most likely be concerned with the SurfaceOfRevolution.cs and HierarchicalModelling.cs files to implement the two requirements. The rest of the project simply provides the UI and tools for verifying your implementation

## Surfaces of Revolution
In this project, you will implement a surface of revolution by creating a triangle mesh. For each mesh, you define a list of **vertices** (the points that make up the primitive) with normals and texture coordinates, and an array indices specifying triangles. Refer to Unity doc's on how to create a triangle mesh: https://docs.unity3d.com/ScriptReference/Mesh-triangles.html
### Surface Normals
**Surface normals**  are perpendicular to the plane that's tangent to a surface at a given vertex. Surface normals are used for lighting calculations, because they help determine how light reflects off of a surface.

We often want to approximate smooth shapes like spheres and cylinders using only triangles. One way to make the lighting look smooth is to use the normals from the shape we're trying to approximate, rather than just making them perpendicular to the polygons we draw. This means we calculate the normals for each vertex (per-vertex normals), rather than each face (per-face) normals. Normals are supplied to Unity in an array in the same order and size that the vertex positions array is built. Hence, the vertices and normals arrays are parallel arrays. Shaders allow us to get even smoother lighting, calculating the normals at each pixel. You can compare these methods below:

![Per-face](https://courses.cs.washington.edu/courses/cse457/20au/img/modeler/flat.png)

##### Per-face

![Per-vertex](https://courses.cs.washington.edu/courses/cse457/20au/img/modeler/gouraud-interp.png)

##### Per-vertex

![Per-pixel](https://courses.cs.washington.edu/courses/cse457/20au/img/modeler/phong-interp.png)

### Texture Mapping
Texture mapping allows you to "wrap" images around your model by mapping points on an image (called a texture) to vertices on your model. For each vertex, you indicate the coordinate that vertex should apply to as a 2D pair (U, V) or (S, T) where U or S is the X-coordinate and V or T is the Y-coordinate of the point on the texture that should line up with the vertex. UVs are passed as a giant array in the same manner (order and size) normals and vertex positions are:
### Using Textures In Your Model
When you want to use a texture, you'll need to do the following:

1.  Import a texture into your scene by dragging an image into **Assets** in Unity.
    
2.  Create a new Material and set its **Albedo** property under **Main Maps** to be the texture.
    
3. Apply the Material to your mesh GameObject by dragging the Material into the GameObject itself.
### Verifying your implementation
To verify the correctness of your implementation, follow this steps:

1.  Ffrom the curve drawing menu, select "Load" and choose our provided file "sample_curve_1.txt" or "sample_curve_2.txt"
2. The points will be loaded. Click "Create" to draw the surface of revolution. Observe if the output from your project is the same as the solution
    
## Hierarchical Modelling
### Model Requirements
For the artifact, you will create a Hierarchical Model. Create a hierarchy of nodes, a combination of Empty nodes and Shape nodes. In Animator, you will end up animating your Model (or you can create a new one) by manipulating the set of transforms and other properties on all these nodes over time.
While it does not have to be a masterpiece, we have 2 requirements:
- #### The model must have at least two levels of branching  
What this means is that if you have a torso, and attach two arms to it, this is one level of branching. The torso splits into each arm. If each arm then has three fingers, that is two levels of branching, since the arm splits into fingers. Note that if you only have one finger, then that does not add additional branching! Below we show two bad (left, middle) and one good (right) examples to help you further understand the "at least two levels of branching" constraint.

![Branching Example](https://courses.cs.washington.edu/courses/cse457/20au/img/modeler/2-levels-of-branching.jpg)


- #### The model must demonstrate two basic human movements 
	In Play mode, your model must automatically perform some animations relating to their joints. In other words, you need to continuously update the Rotation property for these joints to rotate them around some angle. In addition, you can also modify the Position and Scale properties as well to make your model demonstrate some interesting actions. Therefore, we recommend setting up a humanoid model with at least 2 levels of branching as stated above to make your animations of choice. The animations can be basic human movements such as walking, running, and jumping, or other funny cartoonish movements.
	
#### Tree Diagram

Writing down a tree diagram that illustrates the model hierarchy and describes the transforms that each node has can be very helpful in designing a model. Here is a very barebones example of the tree diagram of a simplest robot arm, consisting of two long boxes with a single joint in the center. Note that this example only has one level braching, which means it does not have the required amount of branching.

Note you  **do not**  have to submit a diagram of your model. This is just a recommendation, not a requirement.

![enter image description here](https://github.com/akkaneror/CSE457-Spec/blob/master/image.png)![Simple Hierarchy](https://courses.cs.washington.edu/courses/cse457/20au/img/modeler/simplehierarchy.png)

A tree diagram for this model would look like this:

![Simple Hierarchy Tree Diagram](https://courses.cs.washington.edu/courses/cse457/20au/img/modeler/treediagram.png)

#### Model UI

When demoing your model, or when keyframing it for your animation, you don't want to be clicking down into different hierarchy nodes all the time in order to reach the right properties. You could instead automate the animation by changing its Transform component over time.

For example, in the simple hierarchy above, clicking down into the "A2 Container" node each time you want to change the joint angle is somewhat tedious (and will only get harder with more complex hierarchies). For this requirement, you will find a way to 


The easiest way to do this is to create an empty node, that is your root node, at the top level of your hierarchy, which will serve as a container for your Hierarchy UI. Then, you can implement a UI component and attach it to the root node to help you control the model, without tediously going down the tree to apply the transforms.

Refer to the MazeGame tutorial on how to link the GameObject variables in your script to the actual GameObjects in the Scene. After the linking is done, you can access a GameObject's transform component to modify.

We offer a model sample animation for your reference (bunny_animation)

## ARCore (TBD)
This is what it will look like to import your artifact into our AR app.
![AR Scene of your ArtifactSneakpeak
![enter image description here](https://github.com/akkaneror/CSE457-Spec/blob/master/image.png?raw=true)
### Instruction
1. Export your artifact as a UnityPac
	a. Under Unity **Project** tab, create a new folder and name it "**Prefabs**."
	b. In the Hierachy tab, first click on the root of your artifact, then drag it into the **Prefabs** folders. A confirm dialog will appear, select**Original Prefabs.** Name it anything you'd like.
	c. Right-click on your newly-created **Prefabs**, select Export Pakage. Another window will appear. Deselect everything and only check the Prefab you want to export. Click on "Export.." and choose a destination. 
2. Import your artifact
	a. Open the ARScene Project (where to download is TBD). Navigate to the folder where your Prefab locate, it should look like \<prefab_name\>.unitypackage. 
	b. Double click on it to import the package to our current project. The import package should locate under Prefabs folder. 
3. Connect Prefab to the app. 
	a. First, let's add three component to our Prefabs by clicking on it, Select "Add Component." Three components we should be adding are: Lean Drag Translate, Lean Pinch Scale, and Lean Twist Rot

## Turn In
### Code
Refer to the class's Submission guide to commit and push your final version of the project.
### Artifact Submission
For the artifact, you will create a Hierarchical Model using modeler. As described above, this model must have at least two levels of branching. Also,  **please DO NOT download meshes from the internet as part of your model.**  _Each person must submit their own Hierarchical Model!_

To get full credit for the artifact, your model needs to run automatically when we click "Play" and demonstrate two animations related to your hierarchical model

#### Description

Modeler is a 3D modelling program that lets you design and edit 3D scenes, similar to tools such as Maya, 3DS Max, and Blender. In Modeler, you can set up and arrange 3D elements in a scene, as well as determine their appearance based on the scene's lighting conditions. In addition, in Project 4, you will extend this program to animate your scene, that is, specify how the scene's contents move and change over time.

You'll be implementing many of the core elements of this program, spanning the areas of geometric modelling (specifying the basic 3D shapes of objects in the scene), geometry processing (editing or refining the 3D shapes of objects to achieve certain goals), hierarchical scene modelling (specifying the relative arrangement of objects in the scene), and shading (specifying the appearance of the objects). There are  total requirements:

-   **Geometric Modelling**: Constructing Surfaces of Revolution
-   **Hierarchical Modeling**: Creating Hierarchical Modeling**: eatin 

### Requirements

----------

Implement the features described below. The skeleton code has comments marked with  `// REQUIREMENT`  denoting the locations at which you probably want to add some code.

-   #### Surface of Revolution
    
    Write code to create a 3D surface of revolution mesh in the  **SurfaceOfRevolution::CreateMesh**  method in  **scene/components/surfaceofrevolution.cs**. Your shape must:
    
    -   have appropriate positions for each vertex
        
    -   have appropriate per-vertex normals
        
    -   have appropriate texture coordinates for each vertex
        
    -   have appropriate vertex connectivity (triangle faces)
        
    -   use the "subdivisions" argument to determine how many bands your surface is sliced into.
    
- #### Hierarchical Modeling
    
    Your artifact for this assignment will involve creating a hierarchical model. This model must have at least two levels of branching.
    
    There are two parts to this requirement:
    
    -   Your artifact for this assignment will involve creating a hierarchical model. This model must have at least two levels of branching.
    -   Implement a UI to control the relevant joint transformations of your model.
    
    As part of the project submisson, you need to save your model as YOUR_NETID.yaml, put it in the folder "Editor/assets/model" (you need to create this), and commit to your repository. We will use that model to do grading.
    
    We recommend you can write down the tree diagram of your model to help you figure out what your model will be, and to practice thinking about empty nodes, centers of rotation, and so on. But note the tree diagram is not a requirement.
    
    The UI requirement gives you an easy way to show off your model and makes it much easier to animate. It also will help you learn how to add UI elements to the application.
    
    [Below](https://courses.cs.washington.edu/courses/cse457/20au/src/modeler/modeler.php#hierarchy)  we offer more examples and information to help you figure out how this works.

### Program Usage

----------

The  **Hierarchy**  tab in the left pane represents all the objects in the current Scene. A child object inherits the transformations applied to the parent object like in a scene graph. Parent-Child relationships can changed by simply dragging the objects around in the pane. You may also find creating Empty objects as parents to be useful in building your model. Double click an object to change its name.

The  **Assets**  tab in the left pane represents things like Textures, Shaders, Materials, and Meshes used by the Scene. Materials use Shaders, and shaders use .vert and .frag files. You can either edit them in the right-side Inspector, or choose to create a new asset. Together, the Assets and Scene Graph form a "Scene", and can be saved out or loaded from disk.

  

Selecting an asset or an object will display their properties on the right side in the Inspector. Here you can change their properties, assign different textures, materials, etc. For scene objects, you can also hide them from the hierarchy by unchecking the box by their name.

Modeler uses a component based system for scene objects. Every object has a "Transform" component that represents their Translation, Rotation, and Scale in 3d space. Most rendered objects will have a "Geometry" that defines the shape of the object, and a "Mesh Renderer" that uses a "Material" asset to define how to render that shape. Lights will have an additional "Light" component that defines the light properties.

**Console**  at the bottom is mostly for debugging purposes, at any time in your code, you can call  _Debug::Log.WriteLine_  to print to this console. If you hide the Inspector or any of the other panels in the program, right-click on the tool-bar to show them again.

Scene in the middle is a rendering of your Scene Graph. You can change how its rendered as points, wireframe, or fully shaded via the menu bar along the top of the scene view. If you are having trouble with the orientation of the Perspective view, try switching to an Orthographic view.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc3OTc0ODY0MiwtNjA4ODkzNDQ0LDE2Mj
czMTQ4NDAsMjA1MjcwNDI4OSwtMjgxODMxNzE2LDg4Njk4MTYy
MF19
-->