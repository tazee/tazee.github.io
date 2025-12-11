---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
permalink: /yt-tools/release_1_6.html
---
# YT-Tools for Blender v1.6 Release Note

## ✨ New Features Overview

### 🔹 External Clipboard
**External Clipboard** allows you to exchange mesh data between Blender and Modo.
When **Use External Clipboard** is enabled, copied mesh data is output to the external clipboard specified by **Type** instead of the add-on's internal cache. Using the Modo Clipboard kit, you can exchange mesh data between Modo and Blender via this external clipboard. Mesh data is converted to JSON-formatted text data and output to the external clipboard. The default **Type** of the external clipboard is a temporary file, but specifying OS Clipboard will save the JSON text to the OS-provided clipboard. This is useful for viewing output data or saving it as a file. The mesh information output from Blender is almost the same as the above items. For information on data that can be input into Modo, please refer to the Modo Clipboard kit documentation. The **ModoClipboard kit** is available from [Gumroad](https://tazaki.gumroad.com/) or [Github](https://github.com/tazee/ModoClipboard/releases) download site.
<div align="left">
<img src="images/ExternalClipboard.gif">
</div>