**Intro**
- shade in shading workspace
- you can edit shaders for different materials and the world
- windows:
  - file browser: easy access to files to drag into the workspace
  - image view: view images
  - viewport: set in viewport shading to preview shading
  - shader editor: shader nodes for object and world
  - outliner
  - properties
- you can drag in an image for reference, adding to the viewport, or as a texture node
- render engines:
  - eevee: real-time render
  - cycles: slower, more accurate lighting
  - workspace: preview render (quick animation render)
 
**Shading editor**
- there are multiple starting nodes
- all nodes converge to a single ending point
- drag image into shader editor to create an image texture
- drag color node into another color node to display texture on object
- you can add two shaders together by using the mix RBG node
- draggin a node over connections will insert the node between the connection
- you can mute nodes to quickly see the comparison (m as hotkey)
- delete with reconnect is an option for deleting nodes and not having to reconnect stuff
