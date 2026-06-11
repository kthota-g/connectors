# ARDS connectors

Client-side connectors that let a chatbot **discover agentic resources** — tools,
skills, MCP servers, agents, and APIs — by searching [ARDS](https://ards.io)
discovery services such as **Agent Finder**.

These connectors are **client-side only**. The discovery service (e.g. Agent
Finder) exposes the HTTP `POST /search` and the remote MCP interface; this repo
contains no server. Each connector just points your chatbot at an Agent Finder
endpoint you choose.

## The contract — what every connector does

Every connector follows the same flow (canonical text:
[`shared/discovery-instructions.md`](shared/discovery-instructions.md)). Nothing
is installed automatically:

1. **Ask first** — when you ask it to find tools/skills/agents for a task, it
   asks **which Agent Finder endpoint(s)** to query.
2. **Query** those endpoints (`POST /search`).
3. **Present** the ranked results for you to review (relevance score is *not* a
   trust or safety rating).
4. **Never auto-installs** anything.
5. **Installs only on request** — once you pick a result, it shows you how to add
   that resource yourself.

## Two ways to connect

- **Skill** — a portable instruction bundle that drives the flow over HTTP. Works
  on platforms with a "Skills"-style mechanism and an HTTP/Action capability.
- **MCP** — add an Agent Finder **remote MCP** connector so the chatbot gets a
  native search tool, paired with the Skill for the behavior.

## Per-platform connectors

| Platform | Skill | MCP |
| --- | --- | --- |
| **Claude** | [`skills/claude/`](skills/claude/) | [`mcp/claude/`](mcp/claude/) |
| **ChatGPT** | [`skills/chatgpt/`](skills/chatgpt/) | [`mcp/chatgpt/`](mcp/chatgpt/) |
| **Microsoft Copilot** | [`skills/copilot/`](skills/copilot/) | [`mcp/copilot/`](mcp/copilot/) |
| **Gemini** | [`skills/gemini/`](skills/gemini/) | [`mcp/gemini/`](mcp/gemini/) |

> Capability notes: ChatGPT Skills and Developer-mode MCP are gated to certain
> plans; the consumer **Gemini app** has neither custom MCP nor HTTP, so use the
> Gemini **CLI** or **API** there. Each folder spells out the specifics.

## Endpoints

Connectors are endpoint-agnostic — supply your own Agent Finder URL(s). The
examples use the public `https://finder.nlweb.ai` (`/search` for REST, `/mcp` for
the MCP interface). Replace these with whatever discovery service you trust.
