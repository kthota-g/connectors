# Microsoft Copilot — Agent Finder via remote MCP

Copilot connects to **remote MCP servers** (Streamable transport). Two surfaces:

> Replace `https://agent-finder.example.org/mcp` with your Agent Finder's MCP endpoint.

## Microsoft 365 Copilot / Copilot Studio

1. In **Copilot Studio**, open (or create) your agent → **Tools → Add a tool →
   Model Context Protocol**.
2. Add a **custom connector** for the Agent Finder using the **Streamable** MCP
   transport and the remote MCP URL.
3. Configure authentication if the server requires it, then add the tool to your
   agent.
4. Put the [interaction contract](../../shared/discovery-instructions.md) (or
   `../../skills/copilot/instructions.md`) in the agent's instructions.

## GitHub Copilot (VS Code)

Add the server to your workspace `.vscode/mcp.json` (see `mcp.json` here):

```json
{
  "servers": {
    "agent-finder": {
      "type": "http",
      "url": "https://agent-finder.example.org/mcp"
    }
  }
}
```

Then open Copilot Chat in **Agent mode** and the `agent-finder` search tool is
available. Add the instructions from `../../skills/copilot/` as repo custom
instructions so it asks first and never auto-installs.
