
#### Description

Modeler is a 3D modelling program that lets you design and edit 3D scenes, similar to tools such as Maya, 3DS Max, and Blender. In Modeler, you can set up and arrange 3D elements in a scene, as well as determine their appearance based on the scene's lighting conditions. In addition, in Project 4, you will extend this program to animate your scene, that is, specify how the scene's contents move and change over time.

You'll be implementing many of the core elements of this program, spanning the areas of geometric modelling (specifying the basic 3D shapes of objects in the scene), geometry processing (editing or refining the 3D shapes of objects to achieve certain goals), hierarchical scene modelling (specifying the relative arrangement of objects in the scene), and shading (specifying the appearance of the objects). There are two total requirements:

-   **Geometric Modelling**: Constructing Surfaces of Revolution
-   **Hierarchical Modeling**: Creating 

### Requirements

----------

Implement the features described below. The skeleton code has comments marked with  `// REQUIREMENT`  denoting the locations at which you probably want to add some code.

-   #### Surface of Revolution
    
    Write code to create a 3D surface of revolution mesh in the  **SurfaceOfRevolution::CreateMesh**  method in  **scene/components/surfaceofrevolution.cpp**. Your shape must:
    
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
eyJoaXN0b3J5IjpbMTk5MDEzOTU5NCwtMjgxODMxNzE2LDg4Nj
k4MTYyMF19
-->