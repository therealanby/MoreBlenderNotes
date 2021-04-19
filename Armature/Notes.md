1. Edit mode
2. Add armature
3. Press e to extend
4. This is done in edit mode to ensure the armature are part of one mesh. If they are added separately in object mode, ctrl-j to join
5. Select one bone(single armature) as the parent/root/base and then shift select another to make into a child. Ctrl-p to create parent-child connection*
6. Do this to all bones
7. In pose mode, the armatures should move as one
8. In object mode, select the armature as the active object and then select the mesh to go with the armature (you can do this by selecting the armature first and then pressing a to select everything else, or shift-selecting stuff and shift-select the armature last)
9. right-click, parent, automatic weights
10. go to pose mode, the mesh should move with the armature


*there are two types of connections: attached and non-attached. Attached attaches one bone to another while non-attached keeps them apart but creates a set-distance
