Too lazy to create new files for each category.
Will document useful notes here. 

Topics:
- [UV Editing](#UV-Editing)
- [Procedural Textures](#Procedural-Textures)
- [Three point lighting](#Three-point-lighting)
- [Render](#Render)
- [Render Settings](#Render-Settings)
- [Rigging](#Rigging)
- [Rigging Process](#Rigging-process)
- [Parenting](#Parenting)
- [Armatures](#Armatures)
- [Constraints](#Constraints)
- [Tracking Constraints](#Tracking-Constraints)
- [Transform Constraints](#Transform-Constraints)
- [Character rigging](#Character-rigging)
- [Export/Import file formats](#Export/Import-file-formats)
- [Inverse Kinematics](#Inverse-Kinematics)
- [Vertex Groups](#Vertex-Groups)
- [Bone Layers and Groups](#Bone-layers-and-groups)
- [Keyframes](#Keyframes)
- [Timeline](#Timeline)
- [Misc](#misc)

### UV Editing
- uv editing workspace
- when you select a face in edit mode, it will only show that face on the uv editor
- in edit mode, there is an uv menu for unwrapping the mesh (useful ones are unwrap and smart uv project)
- there are different unwrapping algorithms useful for certain meshes
- you can mark seams as places to cut when unwrapping (mark seems in UV menu)

### Procedural Textures
- textures that are generated using math

### Three point lighting
- one of the best ways to light something
- three lights 
  - main/key light - defined light source (top-left corner usually)
  - fill light - softens shadows made by key light. the least bright. 
  - rim/back light - cast onto the back. brightest. gives object an outline
- spot light is good for this
- encase object with a cube to set up environment

### Render
- render and viewport sampling: more accurate shading render
- lots of settings mess around with them in viewport shading
- tile settings (CPU rendering: 64 x 64; GPU rendering: 256 x 256)

### Render Settings
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


### Rigging
- rigging is a process of turning static models into animated characters
- definition: the act of assigning objects to another object so that the act of moving one object will affect the other
- example: parenting one cube to another
  - move the parent cube and the child cube will follow
  - child cube can be moved independently 
- you can create more complex objects with constraints and armature objects
- stack order matters in constraints
- armature is another word for skeleton
- place armatures inside a model like bones (connect them where joints should be)

### Rigging process
- probably already took notes on this on a file somewhere in this repo
- in edit mode, create the aramtures (press E to extend one from another)
- in object mode, assign the armatures to the model with automatic weights
- go into weight paint mode to change how each armature affect each object
- you can create a bone to point to another bone that acts as a controller
- the controller doesn't deform the mesh directly but controls another bone that does control the mesh. 
- exists to make it easier and more intuitive to use a rig

### Parenting
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

### Armatures
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
- bone property/viewport display/ turn on in front - easier to see bones through mesh

### Constraints
- allows simple and complex relationships to be formed between bones and objects
- object and bone constraints (bone constraints are same as object but assigned to bones)
- constraints
  - copy location: an object with this constraint will have the same location as a chosen object at the specified axis. click x on influence to keep location data after removing constraint
  - limit location: does not depend on an object. Uses values inputted by user. restrains location of object to certain area. check for transform to make the true location also be limited
- note about bones: work similarly. however, you can select individual bones as something to copy as a restraint [10:50 of this vid as example](https://www.youtube.com/watch?v=fx33sPEAZEk&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=32)
- to add a bone as a constraint, add a bone constraint to constrain to individual bones rather than the whole armature object

### Tracking Constraints
- tracking constraints make one object point to another object in some way
- track to will track an object to another object by making one of its axis point to the other object (one use of this is to make another object "look" at another object)
- lock track will track an object to another object but only along one axis
- stretch to will make the object stretch or contract base on its location to the selected object
- damped track is similar to track to but with less options and smoother tracking
- clamp to only works with curves. Clamps/limits object location to the curve. Useful for keeping an object on a certain path during animation

### Transform Constraints
- copy location - if the location of one object is changed, the other object will change in a certain way
- copy scale - if one object is scaled, the other object will scale in a certain way 
- copy rotate - if one object is rotated, the other object will also rotate in a specified way 
- If you want to get really unique and have the location/rotation/scale affect the location/rotation/scale of another object, use the constraint transformation
- you can map from the selected object to the target object. You can select location/rotation/scale to affect the location/rotation/scale. There is a min and max put in place for both to control how much movement/rotation/scaling will affect the other object
- select extrapolate to remove limit and just keep ratio
- you can change source axis to change what axis changes what
- new constraint: limit distance - puts a limit on how far away an object can be from another object or how far an object has to be away(a leash/boundary basically)
- maintain volume - will distort shape when scaling to preserve volume

### Character rigging
- Add-ons/rigging: rigify
- This add on adds some armature templates
- also adds rigify buttons in object data properties
- generate rig creates constraints, bone shapes and other advanced tools automatically
- the rig generated is based off the armature you made. You can delete the armature now, it was made mostly for reference for the auto-rig
- parent the mesh to the generated rig. It doesn't have any bones because the look is changed into those widget/gizmo/thingies. You move around those thingies to change the mesh

### Export/Import file formats
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

### Inverse Kinematics 
[link](https://www.youtube.com/watch?v=S-2v_CKmVE8&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=36)
- Inverse Kinematics(IK) is an important bone constraint
- makes moving limbs and other joints very intuitive
- IK is opposite of forward kinematics(FK)
- bone chains work with FK by default
- FK: moving parent, moves child. Transformations are applied forward down the chain(head to tail)
- IK is when the child bone have influence over its parent bone in some way
- press N and select auto-IK in pose options to see IK in action
- example of IK application: moving the hand(child bone) upwards, the parent bones will also move upwards. In FK, the hand will just rotate up
- auto-IK is nice for quick posing but doesn't give full control
- Have to use IK bone constraint to set it up
- steps:
  1. Pose mode
  2. select a bone
  3. give it the IK constraint in bone constraints
  4. target: armature that the bone is part of, bone: bone to influence
  5. edit mode, disconnect bone to influence
  6. change chain length to change how many bones are influenced
  7. a loop is kinda formed by now. That's why the arm is unstable. Cyclic dependency is what this is called. To change this: edit mode/clear parent
  8. new problem: hand can now be stretched away from arm. To work around this, reparent hand, duplicate hand bone, and unparent the duplicate. Then set the IK to the duplicate to have it act as a separate controller. Now you have one bone that is connected and can be moved around as a hand and one bone that is separate and acts as a controller of the forearm using IK. 
  9. Another problem: hand has to now be rotated separately from the arm. Add a copy-rotation restraint(in pose mode) from the controller to the hand bone. 
  10. Making the IK bone bigger or giving it a custom shape(change it in bone properties)is nice.
  11. arm bends in the wrong way. In IK contraint options, set a pole target. The pole target is a reference object that the elbow/IK joint will try to point to as bones bend. Make a pole target(a bone is fine. It just references by position). Also if the bones are too straight, it will not know which direction to bend
  12. Adjust pole angle value to make sure joint is pointed to the pole correctly

### Vertex groups
[link](https://www.youtube.com/watch?v=dKZrzG5r13g&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=36)
- vertex groups are a groups of vertices that can be referenced for a variety of purposes
- foundation of how a mesh and armature will interact with each other
- each important bone in an armature will have a group of vertices assigned to it
- allows bones of armatures to control a specific part of a complex mesh
- also known as weights
- weights also can control how much influence a bone have over certain vertices
- select mesh, weigth paint mode
- hotkeys: ctrl-Lclick to select bone region. g/r/s to transform. 
- make deformation made by bones more organic and natural
- **how to make/change vertex groups?**
- view vertex groups in object data properties in the properties tab
- assigning automatic weights will create vertex groups automatically with proximity based weights
- the auto generated vertex groups will be named after the bone it is associated with
- in weight-paint mode, there are colors that represent bone influence
  - blue = 0%
  - green = 50%
  - red = 100% (1.0/max value)
- cycle through each group in object data tab to choose which one to display and edit
- select both armature and mesh and go into weigh paint mode to see both. The armature is in pose mode and ctrl-Lclick to select specific bones
- your cursor is now a circle. That is your brush
- you can paint weights
- different tools(press t to display) and tool settings to view tool(press n)
- weight is amount of influence (1.0 = 100%, 0 = 0%)
- strength for mixing (<1 to mix, 1 to completely replace)
- press f to change radius of brush
- options:
  - 2D falloff - with frontfaces on, it will act as spray can. with it off, it will paint all the way through
  - front faces only - only paint on front facing vertices (hidden faces will not be painted) (good for crevices or folds)
- you can apply and remove weights in edit mode
- tools
  - blur - mix weights
  - average - average weight percentages
  - smear - smear weights to other areas
  - gradient - makes a gradient and blends 
  - sample - quickly select weights
- uses
  - modifiers
  - particles
  - physics
  - more
- steps: (time stamp start: 1:45)
  1. make a cube
  2. make an armature for the cube
  3. parent with automatic weights
  4. go to weight paint mode to view vertex groups (select a mesh first)

### Bone layers and groups
[link](https://www.youtube.com/watch?v=MVl7FQw-x6M&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=37)
- bone layers for organization
- layers is located in object data properties (green stick figure)
- basically an outliner except a limited amound is allowed
- used to control which bones show up in view
- useful for complex rigs where organization is necessary
- click to exclusively select a square and shift click to select multiple
- small white dot indicates that there are bones present in that layer
- enable the white dot squares to make those bones visible
- to move bones into layers, go into pose mode
  1. select bones in pose-mode
  2. go to pose menu (top)
  3. change bone layer option
  4. a menu will pop up with the squares. Select the square(layers) which you want the bones to show up
- only one square will have a filled white dot. That means that layer is where the last selected/active bone is
- beginners don't have to worry about the protected layers
- protected layers are used for importing and is used as reference/proxy
- bone groups is located below bone layers
- similar interface to vertex groups
- plus button to add a new group
- select group, select bones in pose mode, and assign
- easy to select/deselect bones in that group
- you can change the color of the groups for more visual clarity

### Keyframes
[link](https://www.youtube.com/watch?v=SZJswvw9wEs&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=38)
- frames are still images. fps is number of frames per second shown in sequence
- a sequence of frames create moving scene
- keyframes are key frames in a moving image
- these are set manually by a person 
- keyframes are where key poses of the character lie
- the frames between keyframes can be blended/interpolated automatically by the software (aka tweening)
- keyframes bascially work the same for objects, bones, materials, and several other values
- there are three keyframe editors: graph editor, dope sheet, and the timeline.
- timeline is the default
- to insert keyframe:
  - right click/insert keyframe on a value (if it doesn't show up, then it can't be keyframed). the value will turn yellow, meaning that there is a keyframe for that value. The keyframe will also show up in the keyframe editor you're using
- keyframes in an editor shown up as yellow shapes (usually squares but can be diamonds or circles)
- loc/roc/scale is good keyframe option because it turns the location, rotation and scale of the object into a keyframe
- white button in timeline to allow auto-keyframing. when you apply a transformation, a keyframe will automatically be generated
- to insert more keyframes, move the frame of the timeline to a different position 
- interpolation can be tweaked in the dope sheet or graph editor
- select keyframes in the editor to delete them
- keyframe type is another term for keyframe color. Used for organization

### Timeline
[link](https://www.youtube.com/watch?v=o19U-yPGdyY&list=PLa1F2ddGya_-UvuAqHAksYnB0qL9yWDO6&index=39)
- change end frame for quicker looping 
- zoom on timeline with scroll wheel
- middle click drag or ctrl+scrollwheel to pan timeline
- right click/duplicate to duplicate keyframes
- default interpolation in blender is a smooth ease in and out motion (slow transition of velocity)
- 

### Misc
- to make custom control thingies, go in object mode, create a circle mesh (not UV sphere) and edit it in edit mode a shape you want. 
- in bone properties, go to viewport display, custom shape, and select the object as that mesh. If it's too big or small, scale it to bone length 
- alt-R and alt-G to reset in pose mode
- 
