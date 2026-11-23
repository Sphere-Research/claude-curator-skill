---
name: "cozmos-curator"
description: "Instructions on how to use the Cozmos Curator MCP"
---

# Core guidelines

Curator provides an MCP in `document.modelContext`.
Avoid using browser debug for curator work when at all possible. Use `capture-`  MCP tools to look at the canvas and various assets. Do not simulate clicks or mouse movements, use direct MCP tools instead. If the necessary MCP tool is missing, mention the limitation to the user, and only simulate manual actions when the user approves it.
Run `snapshot` once after every prompt, to allow the user to undo/redo your work
When starting from an empty sphere, run `planogram-save` yourself after every prompt. If there was an existing design, save only when requested by the user, but prompt them to save periodically.

# MCP API use example

```
const tools = await document.modelContext.getTools();
const tool = tools.find(t => t.name === 'get-object');
const json = await document.modelContext.executeTool(tool, { uuid: '…' });
const result = JSON.parse(json);
```

# Curator overview

Curator is a 3D website builder. The canvas is a complete loop horizontally: X=0 and X=10000 are the same point. The final website is curved, which obscures a significant part of the canvas.
There are upper and lower limits to the Y coordinates, and even within those only a part is genuinely visible. Query the `get-scene` tool to find out the exact visible planogram Y limits. Base your designs around that, and utilize the `toggle-3d-preview` tool to validate the design as you go.

# Uploading assets

Avoid bothering the user with local folder requests if possible. There are MCP tools to upload directly from a web URL. However in case of CORS issues, you may have to save the files into a local directory (make a new one inside Downloads if you can), then use the local folder tools to upload the files from there.

# Styling and colors

When creating a design, or using a design system, prefer to use palettes and numerical colors, instead of hex colors directly. Do not create large palettes, stick to 12 or fewer colors. Any extra colors can be set as hex codes, if they are necessary.
