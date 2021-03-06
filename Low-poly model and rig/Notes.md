# Modeling
## Setting things up
- Nice add-on to have: auto mirror
- one cube

## Steps
- select mesh, press n(side bar), edit tab, auto mirror dropdown, select x and click auto mirror
- in edit mode, any changes in the mesh will be applied to the other side of the mesh across the y axis
- make a pelvis
- convert to torso by draggin face up
- add two loop cuts to split the torso into three
- create a small loop cut near the bottom segment (used for the legs)
- select bottom right edge and move it inwards
- e to extrude bottom face 
- scale the face
- r to rotate and make the face parallel to ground
- g to move the leg stumps
- extrude bottom face again to make legs all the way to the kneecap
- press g, z, and 0. This flattens the face to the z-axis I think
- extrude a small region twice for the knee. Twice for easier rigging. (two knee lines for bending is weird, three is better)
- extrude again for lower legs
- extrude again for ankle
- extrude from ankle twice for feet
- extra: create a loop cut, slide it to where you want the pant edge to be, scale it for pants leg effect
- upper right face on the side of the torso, select it
- extrude it a little for the arms
- scale down face
- move it up so it somewhat matches with shoulder(not totally in-line. Just lined up with shoulder in a slanty way like a real shoulder)
- extrude once for arms(should be a t-pose)
- scale down arm
- extrude twice for elbows
- extrude and scale for other arm segment
- extrude, scale up and extrude again for simple blocky hands
- extrude from top of torso to start forming head
- scale and grab/slide inwards for neck base
- extrude for neck
- extrude and scale for head
- grab head outwards to make the base more square
- grab head out more for cartoon bighead
- extrude for rest of head
- loop cut with # of cuts at 2
- select edges at bottom and top of head to scale them down to make the head more detailed
- grab the faces inwards for rounder head shape
- edge select for more body detail
- select three chest edges. grab them out in a way to make a belly
- bring out side edge for waist
- arch the back and bring the back shoulders up
- belt: loop cut, scale out, loop cut below, scale out, scale/grab edges for additional detail, bring back that pointy vert at crotch
- loop select belt and extrude along normals
- head shrinking: box select in x-ray mode, scale down/up, and move down/up
- color: download palette provided by video (very small image to keep file size down)
- shading tab
- drag palette into node shader editor and connect to base color
- set interpolation from linear to closest
- go to UV editing workspace
- set viewport shading color to texture
- 'a' to view uv on palette texture and scale it down to zero. (a, s, 0)
- moving the dot to change color
- now you can select colors for faces
- select face on side of the head. shift-d to duplicate. scale down into a base for an ear. Extrude for ear
- select face on front of the head. go to modifiers and disable clipping. Scale down for eyes. 
- loop-cut for pupils
- e to extrude eyes
- hat: duplicate faces on head, enable clipping, scale up and model into however style you want
- right-click, separate by selection to separate from person mesh
- select bottom edges and press f to fill in a face
- loop cut and extrude can be used for caps visors
- inset to create faces to color
- edge slide!
- vertex slide!
- customization: duplicate person body. hide the original body and hat
- select linked and uv in final operations menu to select faces of same color
- edge loop select to widen/tighten parts of the body 
- loop-cut and inset for creating faces to color

# Rigging
## Setup
- Low-poly model

## Steps
- front-view, have nothing selected, shift-space, add armature/bone
- edit mode for armature
- move head to crotch area and move tail to the top of the pants
- press e and z to extrude on z-axis. do this twice to create a spine
- rename: root, spine1, spine2, head
- extrude from head of head bone for shoulder bone and arms (do this for each arm)
- move elbow back a bit so it's not straight-locked (IK-solver)
- rename bones
- extrude one bone from the head of the root and move it to the left leg
- make leg (3 bones) and make sure the knee joint is bent forward a little
- rename (upperLeg.L, lowerLeg.L, foot.L)
- armature/bone roll/recalculate roll (shift-n)/view axis (doesn't seem to do much but will help later) (will help know which way to fold bones)
- time to set up inverse kinematics before mirroring
- extrude from knee and heel and clear their parents
- move them out and rename them IK pole bone (inverse-kinematic pole bone) (purpose to to know where to aim the joints) 
- deselect deform of the pole in bone properties
- go into pose mode, and go into bone constraints for the lower leg bone
- add inverse kinematics
- select the heel IK bone as target and knee IK bone as pole target
- in edit mode, connect upper leg to root by select bone (select root last) and create parent(ctrl-p) as offset
- set chain length to 2 in IK and set pole angle to 90 degrees
- what has been done: if you move the target IK bone, the leg moves like a leg(knee bends correctly). If you move the root, leg will also move and bend correctly
- click on foot bone, go to bone-properties/relations and disable inherit rotation. The foot won't rotate now when the other bones are moved. 
- still on foot bone, add copy rotation constraint and copy it to the IKTarget bone. set target and owner to local space and invert z and y axis
- edit mode, select all, armature/symmetrize (make sure bones are name with .L or \_L suffix so it can create a corresponding .R)  
- select character and shift-select armature. go to object/parent/auto-weight (armature deform) or ctrl-p, armature deform-auto-weights
- eyes are weird and some parts may also bend weirdly
- automatic weight applied weights from the verts of the mesh to the armature
- in edit mode, in the context menu(hotkey n) after selecting a vertex, you can edit vertex weight in item tab
- you should probably use weight paint mode
- remove eye verts (select linked) in vert/vert-groups/remove-all
- set and assing to active group: head
- hat: add child of constraint and assign it to the armature and head group (click set inverse to set right position)

# Animation
## Setting things up
- animation workspace
- viewport shading: texture, shadow, cavity(both) (sliders all the way up) (crisper mesh)
- rig
- armature set to x-ray for easier posing
- dope-sheet to action editor

## Steps
- **Idle Animation**
- create new action and name it TPose
- lower arms
- lower root so that knees are a little bent
- adjust knees a bit
- adjust feet a bit
- this is frame 0/1 (i prefer to start from 0)
- move to frame 20
- adjust root up a little 
- move shoulders up a little and arms down to account for shoulder movement
- optional: rotate the spine bones a little
- duplicate keyframes from frame 0 to frame 40
- cyclic movements (predict motion curves)
- select all keyframes and go to channel/extrapolation mode (shift-e) and make cyclic
- new animation named run. duplicate idle
- alt-g and alt-r to reset pose
- get a run cycle reference and start making key frames based off the reference you chose
- that's pretty much it. adjust other bones to your liking. 

## Hot keys
- 1 on numpad to get good front view for mirror modeling
- 3 on numpad for side view
- n for sidebar
- shift-space for quick menu of tools (g for grab, r for rotate, s for scale)
- alt-z for x-ray vision (useful for better view and selection of hidden things)
- alt-click (face mode) for loop select (selects a loop of faces)
- ctrl- + (numpad plus) for selection grow
- shift-c to reset 3D cursor
- select verts/edges and press f to fill (create new face)
- f2 - rename
- select bones and press shift-n to recalculate rolls


## Tips
- 2 units is a good size for a video game model
- for bending parts of the mesh for the rig, have three or more lines for better bending
- enable clipping in mirror mod so there are no gaps at reflection point
- import palette as texture (node editor). Editing UV so that everything becomes a dot(scale to 0). Move dot around to select color. Select faces and moving the dot will change the face color
- viewport shading: backface culling makes the back of a face invisible
- you can fill verts/edges by going into vertices/(new edge/face from vertices)
- edge/edge slide for sliding an edge along an edge during grab operation
- enable in front in bone-properties/viewport-display for easier bone editing
- number your action frames(animation) so they appear alphabetically in programs
- end one frame before actual keyframe so looping looks nicer
