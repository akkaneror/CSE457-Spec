
#### Description

Modeler is a 3D modelling program that lets you design and edit 3D scenes, similar to tools such as Maya, 3DS Max, and Blender. In Modeler, you can set up and arrange 3D elements in a scene, as well as determine their appearance based on the scene's lighting conditions. In addition, in Project 4, you will extend this program to animate your scene, that is, specify how the scene's contents move and change over time.

You'll be implementing many of the core elements of this program, spanning the areas of geometric modelling (specifying the basic 3D shapes of objects in the scene), geometry processing (editing or refining the 3D shapes of objects to achieve certain goals), hierarchical scene modelling (specifying the relative arrangement of objects in the scene), and shading (specifying the appearance of the objects). There are five total requirements:

-   **Geometric Modelling**: Constructing Surfaces of Revolution
-   **Geometry Processing**: Mesh Smoothing
-   **Hierarchical Modeling**
-   **Shading**: Blinn-Phong Point Light Shader
-   **Shading**: Additional Shaders

### Requirements

----------

Implement the features described below. The skeleton code has comments marked with  `// REQUIREMENT`  denoting the locations at which you probably want to add some code.

-   ##### Surface of Revolution
    
    Write code to create a 3D surface of revolution mesh in the  **SurfaceOfRevolution::CreateMesh**  method in  **scene/components/surfaceofrevolution.cpp**. Your shape must:
    
    -   have appropriate positions for each vertex
        
    -   have appropriate per-vertex normals
        
    -   have appropriate texture coordinates for each vertex
        
    -   have appropriate vertex connectivity (triangle faces)
        
    -   use the "subdivisions" argument to determine how many bands your surface is sliced into.
    
-   #### Hierarchical Modeling
    
    Your artifact for this assignment will involve creating a hierarchical model. This model must have at least two levels of branching.
    
    There are two parts to this requirement:
    
    -   Your artifact for this assignment will involve creating a hierarchical model. This model must have at least two levels of branching.
    -   Implement a UI to control the relevant joint transformations of your model.
    
    As part of the project submisson, you need to save your model as YOUR_NETID.yaml, put it in the folder "Editor/assets/model" (you need to create this), and commit to your repository. We will use that model to do grading.
    
    We recommend you can write down the tree diagram of your model to help you figure out what your model will be, and to practice thinking about empty nodes, centers of rotation, and so on. But note the tree diagram is not a requirement.
    
    The UI requirement gives you an easy way to show off your model and makes it much easier to animate. It also will help you learn how to add UI elements to the application.
    
    [Below](https://courses.cs.washington.edu/courses/cse457/20au/src/modeler/modeler.php#hierarchy)  we offer more examples and information to help you figure out how this works.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NDgzNzExNjcsODg2OTgxNjIwXX0=
-->