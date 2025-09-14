---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
permalink: /yt-tools/release_1_3.html
---
# YT-Tools for Blender v1.3 Release Note

## ✨ New Features Overview

### 🔹 Smooth Brush
<b>Smooth Brush</b> is a transform tool that smooths the coordinate values ​​of vertices within a radius around the cursor with a brushing action. <b>Size</b> is the radius of the on-screen falloff circle, which can be interactively changed by dragging the RMB. Dragging the LMB around the vertices you want to smooth will smooth vertices within the falloff circle. <br><br>
<div align="left">
<img src="images/SmoothBrash.gif">
</div>

### 🔹 Soft Drag Update
<b>Smooth Brush</b> can be used on <b>Soft Drag</b> operator. Shift key and dragging with the LMB will smooth the vertex coordinates within the falloff, which is the same process as the smooth brush. <br>

### 🔹 Workplane Update
<b>Set to 3D Cursor and Rotation</b> sets the rotation matrix of the work plane to the name Cursor in Transform Orientations and the position coordinates to the 3D Cursor in Transform Pivot Position.

### 🔹 Selection Set Update
<b>Replace</b> overwrites the currently displayed <b>Selection Set</b> with the current selection.

### 🔹 Preferences Update
<b>View Navigation</b> has been removed from Preferences panel. Now the view navigation events are automatically recognized in YT-Tools.

### 🔹 Other Changes
- Fixed a bug about display info text after loading a scene.
- Fixed an issue so that Randomize Transform does not work with YT-Tools
- Fixed Add Loop and Loop Slice to show Adjust Last Operation panel.
- Set the initial symmetric state to Merge and Loop Slice 
- Automatically detects view navigation operations and removes the Navigation selection option from the Preferences