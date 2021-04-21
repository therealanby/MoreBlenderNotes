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
