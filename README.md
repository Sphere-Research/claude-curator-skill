# Cozmos Curator

Lets Claude build and edit 3D shperical websites in [Cozmos](https://cozmos.com) Curator, the 3D website builder at [publishingtools.cozmos.com](https://publishingtools.cozmos.com/).
Claude works through the MCP tools Curator registers on the page (WebMCP). It can upload assets and design your sphere entirely autonomously!

New to Curator? See the [Cozmos knowledge base](https://learn.cozmos.com/).

## Setup

> **Temporary workaround.** Claude can't yet use WebMCP tools directly, so for now they reach Claude through the Chrome DevTools MCP server. These steps will go away once Claude supports WebMCP.

You need Chrome 150+, Node.js 20.19+ and the Claude desktop app.

1. **Chrome:** at `chrome://flags/#enable-webmcp-testing`, enable **WebMCP for testing** and relaunch Chrome. Then at `chrome://inspect/#remote-debugging`, allow incoming debugging connections.
2. **Claude config:** in Claude, open **☰ → Developer → Open App Config File** (`claude_desktop_config.json`) and add:

   ```json
   {
     "mcpServers": {
       "chrome-devtools": {
         "command": "npx",
         "args": [
           "-y",
           "chrome-devtools-mcp@latest",
           "--autoConnect",
           "--categoryExperimentalWebmcp"
         ]
       }
     }
   }
   ```

   On Windows, use `"command": "cmd"` and put `"/c", "npx",` at the start of `args`. On Chrome Canary, Dev or Beta, add `"--channel=canary"` (or `dev`, `beta`) to `args`.

3. **Reload:** choose **☰ → Developer → Reload MCP Configuration**. If the tools don't show up, quit Claude fully from the tray or menu bar and start it again.
4. **Try it:** open your sphere in Curator, then ask Claude to list the WebMCP tools on that page. Click **Allow** when Chrome asks.
