---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
permalink: /AttributeManager/index.html
---

<style>
table {
  border-collapse: collapse;
  width: 100%;
}
table, th, td {
  border: 1px solid #ccc;
}
th, td {
  padding: 6px;
  text-align: left;
}
</style>

# Attribute Manager for Blender

The Attribute Manager is a Blender add-on that provides a spreadsheet-style interface for editing mesh vertex, edge, and face attributes, as well as various other object attributes.

It offers a convenient GUI for bulk attribute editing that would otherwise require manual and tedious panel clicks.<br>

## Blender Version

This add-on works with:<br>
- Blender 4.0, 5.0 or later
- It is written entirely in Python and works on macOS and Windows.

## Installation

- Open Blender.
- Go to Edit > Preferences > Add-ons.
- Click Install… and select the AttributeManager.zip.
- Enable the add-on by checking the box next to Attribute Manager.
<div align="left">
<img src="images/installAddon.png"/>
<img src="images/addon.png"/>
</div>
<br>

## How to Use

You can adjust the width of the panel by dragging its left edge.
The number of visible table rows can be changed using <b>Max Rows</b> (default is 6).<br>
<div align="left">
<img src="images/sideBar.png"/>
</div>
<br>

## User Interface Overview
<div align="left">
<img src="images/UI.png"/>
</div>
<br>

### <ins>(1) Correct Selected (Correct Objects)</ins><br>

Pressing Correct Selected loads the currently selected vertices, edges, faces, or objects into the Attribute Manager.
- In Mesh Edit Mode, it loads the selected mesh elements (vertex/edge/face) into the spreadsheet for editing.
- In Object Mode, it loads attributes of the selected objects.
- If you change selection or the mesh structure, press Correct Selected again to refresh the table.<br>

### <ins>(2) Mode Selection</ins><br>
There are four editing modes:<br>
- Vertex
- Edge
- Face
- Object

When switching modes, the currently selected elements are automatically reloaded into the table.
Vertex/Edge/Face modes operate in Edit Mode, while Object mode operates in Object Mode.

### <ins>(3) Attribute Selection</ins><br>
This area lets you select which attributes to display using toggle buttons.
Only selected attributes appear as columns in the editing table.
Use this to focus on only the fields you need.

### <ins>(4) Editing Table</ins><br>
This is the spreadsheet-style table where loaded attributes can be edited.
- Use the vertical scroll bar on the right to scroll through rows.
- The first row shows the attribute names (column headers).
- In Vertex/Edge/Face modes, mesh element indices are shown.
- In Object mode, object names are shown.
- The currently active row is highlighted in blue.

### <ins>(5) Apply to All Rows<ins><br>
The <b>Apply to All Rows</b> button applies the value from the selected row to all other rows for the field chosen in the adjacent dropdown.

### <ins>(6) Show Indices, Show Weights<ins><br>
- <b>Show Indices</b> displays the index numbers of mesh elements in the 3D View.
This performs the same function as the Indices toggle in the Blender Edit Mode overlay.
- <b>Show Weights</b> displays vertex group weights as a gradient in the 3D View.
This matches the <b>Vertex Group Weights</b> overlay setting in Edit Mode.

### <ins>(7) Max Rows<ins><br>
<b>Max Rows</b> sets the number of rows shown in the editing table.
Default value: 6.


## Vertex Edit Mode
<div align="left">
<img src="images/vertexMode.png"/>
</div>
<br>

In Vertex Edit Mode, you can edit:
- Vertex coordinates
- Shape keys
- Vertex group weights

Coordinate values can be displayed and edited in either local or global coordinate space.<br>
When in Edit Mode, global coordinates are converted from local, displayed in the table, and converted back when applied.
This allows precise positioning in global space when needed.

<div align="left">
<img src="images/vertexPosition.gif"/>
</div>
<br>


## Edge Edit Mode
<div align="left">
<img src="images/edgeMode.png"/>
</div>

In Edge Edit Mode, you can edit edge attributes such as:
- Smooth
- Crease

These influence subdivision surfaces, shading, and modeling workflows.

<div align="left">
<img src="images/edgeLength.gif"/>
</div>
<br>

## Face Edit Mode
<div align="left">
<img src="images/faceMode.png"/>
</div>

In Face Edit Mode, you can edit face attributes such as:
- Material slots
- Freestyle attributes

This allows quick assignment or bulk editing of material indices and rendering attributes.

## Object Edit Mode
<div align="left">
<img src="images/objectMode.png"/>
</div>

In Object Mode, you can edit various object attributes, including:
- Display properties
- Transform values
- Object-type specific attributes

When in Object Mode:
- Use the first dropdown to select which object types to load (e.g., Mesh, Light, Camera).
- Use the second dropdown to select the category of attributes to show.

For example, you can group attributes into categories like Visibility, Transform, Display, etc.<br>
Press Apply to All Rows to apply changes to all selected objects.<br>
When applying the same Name to multiple objects, Blender automatically appends numbers to ensure unique names (e.g., “Bone_LeftLeg_001”, “Bone_LeftLeg_002”, etc.).


<div align="left">
<img src="images/objectRename.gif"/>
</div>



## Change Log

### v1.0

- Initial release of Attribute Manager for Blender

## License

This Blender add-on is licensed under the GNU General Public License v3.0 or later.

You are free to use, modify, and redistribute it under the terms of the GPL license.
For details, please see the included `LICENSE.txt`.
