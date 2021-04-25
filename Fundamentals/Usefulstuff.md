Too lazy to create new files for each category.
Will document useful notes here. 

**UV Editing**
- uv editing workspace
- when you select a face in edit mode, it will only show that face on the uv editor
- in edit mode, there is an uv menu for unwrapping the mesh (useful ones are unwrap and smart uv project)
- there are different unwrapping algorithms useful for certain meshes
- you can mark seams as places to cut when unwrapping (mark seems in UV menu)

**Procedural Textures**
- textures that are generated using math

**Three point lighting**
- one of the best ways to light something
- three lights 
  - main/key light - defined light source (top-left corner usually)
  - fill light - softens shadows made by key light. the least bright. 
  - rim/back light - cast onto the back. brightest. gives object an outline
- spot light is good for this
- encase object with a cube to set up environment

**Render**
- render and viewport sampling: more accurate shading render
- lots of settings mess around with them in viewport shading
- tile settings (CPU rendering: 64 x 64; GPU rendering: 256 x 256)

**Render Settings**
- Ambient Occlusion: makes 3d shadows feel more real
- Bloom: glow (color, glow threshold)
- Depth of Field: real life camera effect. Blurred background from focal point (have to select this in camera properties and not render)
- camera/viewport display/limit: turns on focal point and you can adjust it in 3D viewport
- F-stop: lower = less clear things, higher = more clear things
- subsurface is a setting to impact the color glow of something when a bright light is shining through it (I guess kinda like holding a flashlight into your hand and your hand glowing red)
- Screen space reflection: approximate reflective and refractive surfaces
- motion blur: blurs movement in animations
  - tip: circle button on timeline for auto-keyframing with camera
- volumetrics: affect how volumetric shaders look in the scene (volumetric is fog and stuff I think)
- Hair: settings for hair particles
- shadow: different shadow calculations
- Indirect lighting: used to affect light probe objects 
  - light probes are use to pre-calculate lighting effects (surround a reflective object and click bake indirect lighting to show reflections)
  - watch out for clipping. It affects how the reflection is shown on the object (turn on clipping in light probe properties) 


**Rigging**
- rigging is a process of turning static models into animated characters
- definition: the act of assigning objects to another object so that the act of moving one object will affect the other
- example: parenting one cube to another
  - move the parent cube and the child cube will follow
  - child cube can be moved independently 
- you can create more complex objects with constraints and armature objects
- stack order matters in constraints
- armature is another word for skeleton
- place armatures inside a model like bones (connect them where joints should be)

**Rigging process**
- probably already took notes on this on a file somewhere in this repo
- in edit mode, create the aramtures (press E to extend one from another)
- in object mode, assign the armatures to the model with automatic weights
- go into weight paint mode to change how each armature affect each object
- you can create a bone to point to another bone that acts as a controller
- the controller doesn't deform the mesh directly but controls another bone that does control the mesh. 
- exists to make it easier and more intuitive to use a rig

**Parenting**
- important part of the rigging process
- parent-child relationship
- child objects inherit transformations from its parent
- child objects can have its own transformation
- bascially, you move parent, the child also moves. You move child, the parent doesn't. 
- parenting helps easily control transformations and pivot points during animations
- examples: finger to hand, papers to a desk, leaves to a tree
- select object as parent, then select object to parent. right-click/parent/object (ctrl-P) 
- ignore previous bullet, this parents the wrong cube
- do the same thing but select parent object last
- yellow outline is more active than orange (yellow indicates last selected I think)
- you can also change the parent - child relationship in object properties/relations 
- a parent can have multiple children but a children can only have one parent
- you can make parents of other parents
- one parent will affect another parent which will also affect that parent's children
- this parent to parent relation can be as long as you want but it cannot form a loop. This means that a child of a parent cannot parent the parent, grand-parent, or any of the parents that it is connected to
- you can create an empty. They have only data about their own transformations and they don't show up in the render. 
- used for organization and reference
- useful to use as an invisible parent
- example: every object in a classroom is parented to an empty. Moving the empty will move the entire scene
- you can clear parent-child relation by selecting objects and unparenting in the context menu(right-click menu) or going into object properties and removing the relation

**Armatures**
- armature/rig/skeleton
- made up of bones (individual moving parts of a skeleton)
- create, edit and transform bones to animate them
- add in add menu and add armature
- you can edit (tab) and pose (ctrl-tab) the bones
- pose mode is where most of the animation will be done
- a bone is made of three parts (head, body, and tail) (head is pivot point at the wide end)
- you can move the head and tail individually to move those areas, or move the entire bone by moving the body
- two parent options
  - connected(will connect child's head to the tail of the parent bone)
  - keep offset(will not move anything but will create this dashed line between the two. Similar to normal parenting. Will only work in pose-mode however)
- connected is good for making bone chains
- offset good for creating hanging parts like ears
- you can also right-click/subdivide to create multiple connected bones
- E to extrude (extruded bones are connected by default)
- to clear, select parent/clear in context menu
- viewport display of bone properties to view axis. Roll bone tool is used to make sure bones only bend one way
- bone view types (octohedral/default is best)
- you animate in pose mode
- move bones to wanted position, select bones, insert keyframe, and selecting lotrotscal (location, rotation, scale) to make keyframe
- to parent armature to mesh, select mesh, select armature last, and armature deform/with auto weights in context menu
- this creates an assignment of vertices to each bone generated by blender to control general location of mesh to each bone
- vertex groups is what the vertices are called and each bone has a group that they control
- meshes will have an armature modifier

**Constraints**
- allows simple and complex relationships to be formed between bones and objects
- object and bone constraints (bone constraints are same as object but assigned to bones)
- constraints
  - copy location: an object with this constraint will have the same location as a chosen object at the specified axis. click x on influence to keep location data after removing constraint
  - limit location: does not depend on an object. Uses values inputted by user. restrains location of object to certain area. check for transform to make the true location also be limited
- note about bones: work similarly. however, you can select individual bones as something to copy as a restraint [10:50 of this vid as example](https://www.youtube.com/watch?v=fx33sPEAZEk&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=32)
- to add a bone as a constraint, add a bone constraint to constrain to individual bones rather than the whole armature object

**Tracking Constraints**
- tracking constraints make one object point to another object in some way
- track to will track an object to another object by making one of its axis point to the other object (one use of this is to make another object "look" at another object)
- lock track will track an object to another object but only along one axis
- stretch to will make the object stretch or contract base on its location to the selected object
- damped track is similar to track to but with less options and smoother tracking
- clamp to only works with curves. Clamps/limits object location to the curve. Useful for keeping an object on a certain path during animation

**Transform Constraints**
- copy location - if the location of one object is changed, the other object will change in a certain way
- copy scale - if one object is scaled, the other object will scale in a certain way 
- copy rotate - if one object is rotated, the other object will also rotate in a specified way 
- If you want to get really unique and have the location/rotation/scale affect the location/rotation/scale of another object, use the constraint transformation
- you can map from the selected object to the target object. You can select location/rotation/scale to affect the location/rotation/scale. There is a min and max put in place for both to control how much movement/rotation/scaling will affect the other object
- select extrapolate to remove limit and just keep ratio
- you can change source axis to change what axis changes what
- new constraint: limit distance - puts a limit on how far away an object can be from another object or how far an object has to be away(a leash/boundary basically)
- maintain volume - will distort shape when scaling to preserve volume

**Character rigging**


**Export/Import file formats**
- useful(.obj, .fbx, .dae(??))
- 3D model export: .obj, and .fbx
- Best is probably .fbx
- collada/ .dae -  3d model, image, texture
- alembic/ .abc - visual graphics and animation (scene)
- universal scene description/ .usd - scenes I think (scene)
- Stanford/ .ply - 3D data for 3D scanners (vertex/mesh and texture)
- Stl/ .stl - standard triangle language. also used for 3D printing (triangle mesh)
- FBX/ .fbx - 3D geometry and animation
- glTF/ .glb - 3D scenes and models 
- Wavefront/ .obj - vertex data (models)
- X3D/ .x3d - 3D computer graphics 
- Motion capture/ .bvh - motion capture for armature (rig animation I think)
- curves/ .svg - curves
- Toolpath/ .gcode - some programming thing (scripting??)
- ______
- just the mesh: .obj
- also textures: .fbx
- rig: .dae or .fbx
- animation/keyframes: .bvh
- shaders: .glb??
- 2d scene: .svg 


**Misc**
- to make custom control thingies, go in object mode, create a circle mesh (not UV sphere) and edit it in edit mode a shape you want. 
- in bone properties, go to viewport display, custom shape, and select the object as that mesh. If it's too big or small, scale it to bone length 
