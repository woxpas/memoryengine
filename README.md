# Woxpas — Personal Memory Engine

**Your second brain that actually remembers.**

Woxpas is a personal memory engine that transforms your documents into living knowledge. Unlike static file storage, Woxpas understands what you've saved, connects related ideas across documents, and resurfaces forgotten insights exactly when you need them.

---

## Table of Contents

- [What is Woxpas?](#what-is-woxpas)
- [Web App (UI + Backend)](#web-app-ui--backend)
- [MCP Server](#mcp-server)
- [Browser Extension](#browser-extension)
- [Reporting Issues](#reporting-issues)
- [Status](#status)
- [Links](#links)

---

## What is Woxpas?

Woxpas ingests your content — notes, PDFs, documents, audio — and builds a living memory that grows with you. It extracts entities, events, ideas, and commitments from your files, maps connections between them in a knowledge graph, and resurfaces what matters through a daily digest and intelligent retrieval.

**Core features:**

- **Memory Home** — A capture canvas and signals layer showing what's active (Thinking), what's returning (Echoes), and what's forming (Emerging)
- **Knowledge Graph** — Visual map of how your ideas connect across documents, with 5 node types and 11 edge types
- **Smart Retrieval** — Ask questions in natural language with automatic mode selection (meaning vs artefact vs recent recall)
- **Follow-ups & Events** — Automatic commitment tracking with reliability scores and calendar sync
- **Daily Digest** — AI-generated summary of resurfaced memories, upcoming commitments, and emerging patterns
- **Citations** — Every answer links back to the exact source passage in your documents
- **Integrations** — MCP server for AI assistants, Chrome extension for quick capture, Google Drive import

---

### Technology

| Component | Stack |
|-----------|-------|
| **Backend** | Python, FastAPI, async processing |
| **Database** | PostgreSQL with pgvector for embeddings |
| **Search** | Hybrid vector + lexical with reciprocal rank fusion |
| **LLM** | Multi-model (OpenAI, Anthropic, Google) — user-configurable |
| **Frontend** | Next.js (Pages Router), Tailwind CSS |
| **MCP Server** | FastMCP with hybrid SSE + Streamable HTTP transport |
| **Extension** | Chrome Manifest V3 |

---

## Web App (UI + Backend)

The main Woxpas application at [woxpas.ai](https://woxpas.ai).

### What it covers

- **Memory Home**: Upload files, paste text, record audio, save URLs. View resurfaced memories and emerging patterns.
- **Sources**: File management with processing status. Supported formats: PDF, DOCX, TXT, Markdown, audio (auto-transcribed).
- **Explore**: Interactive knowledge graph with search, filtering, and node/edge inspection.
- **Ask**: Natural language search across your entire memory with cited responses.
- **Follow-ups & Events**: Extracted commitments and events with status tracking and calendar subscription.
- **Daily Digest**: Personalised AI-generated email summary.
- **Settings**: 6 tabs — General, Billing & Usage, Data & Privacy, Privacy Dashboard, Security, Developer.

### Known areas to report

If you experience issues with any of the above, please open an issue with the relevant label (see [Reporting Issues](#reporting-issues)).

---

## MCP Server

The Woxpas MCP server lets you use your personal memory from AI assistants like Claude, ChatGPT, Cursor, Gemini CLI, and others.

**Server URL:** `https://mcp.woxpas.ai/mcp/sse`

### Supported clients

| Client | Status | Transport |
|--------|--------|-----------|
| Claude Code (CLI) | Working | SSE |
| ChatGPT | Working | SSE |
| Cursor | Working | SSE |
| Langdock | Working | SSE |
| Gemini CLI | Working | SSE |
| Claude Desktop | Working | SSE |

### Available tools

| Tool | Description |
|------|-------------|
| `capture_messy_intent` | Save content to your memory vault |
| `recall_temporal_context` | Search and retrieve from your memory |
| `resolve_human_logic` | Look up a specific entity (person, project, etc.) |

### Setup

1. Go to **Settings > Developer** in the Woxpas app
2. Connect your AI assistant via OAuth
3. Add the MCP server URL to your client's configuration:

```json
{
  "mcpServers": {
    "woxpas": {
      "url": "https://mcp.woxpas.ai/mcp/sse",
      "transport": "sse"
    }
  }
}
```

### Known areas to report

- Connection failures or timeouts
- OAuth flow issues (duplicate connections, failed reconnects)
- Tool responses that are empty, truncated, or incorrect
- Transport-specific issues on specific clients

---

## Browser Extension

**Woxpas Quick Capture** — Type a note and save it to your memory without leaving the page you're browsing.

**Install:** [Chrome Web Store](https://chromewebstore.google.com/detail/woxpas-quick-capture/ojdndbnblnnompjehingieaemcdhldhd)

### What it does

- Opens a quick capture popup from any tab
- Type a note, thought, or idea
- Saves directly to your Woxpas vault
- No page navigation required

### Known areas to report

- Extension not connecting to your account
- Notes not appearing in your vault after saving
- Popup not opening or closing unexpectedly
- Performance issues while the extension is active

---

## Reporting Issues

We use GitHub Issues to track bugs and feature requests during the beta.

### How to report a bug

1. **Check existing issues** first to avoid duplicates
2. **Open a new issue** with the following details:

```
**Component**: [Web App / MCP Server / Browser Extension]
**What happened**: [Describe the issue clearly]
**Expected behavior**: [What should have happened]
**Steps to reproduce**: [How to trigger the issue]
**Browser/Client**: [e.g. Chrome 120, Claude Code, ChatGPT]
**Screenshots**: [If applicable]
```

### Labels

| Label | Use for |
|-------|---------|
| `bug` | Something isn't working as expected |
| `web-app` | Issues with the Woxpas web application |
| `mcp-server` | Issues with MCP connections or tool responses |
| `extension` | Issues with the Chrome Quick Capture extension |
| `extraction` | Issues with how content is extracted from documents |
| `retrieval` | Issues with search results or answer quality |
| `digest` | Issues with the daily digest email |
| `ui` | Visual or interaction issues |
| `feature-request` | Suggestions for new features or improvements |

### What helps us most

- **Specifics over summaries** — "Clicking 'Save' on the capture popup does nothing" is more useful than "extension broken"
- **Screenshots or screen recordings** when reporting UI issues
- **Your browser and OS** for web app issues
- **Which AI client** for MCP issues (Claude Code, ChatGPT, Cursor, etc.)
- **File type and size** for extraction or upload issues

---

## Status

Woxpas is currently in **Beta**. The core memory engine is functional, but expect rough edges and rapid iteration.

**What Beta means:**
- Core features work but may have bugs
- Performance is being optimised
- Your feedback directly shapes what gets built next
- Data is persisted — we recommend periodic exports for important content

**Current limits (Beta plan):**
- 5 files per upload batch (50 MB each)
- Daily query limits apply
- One vault per account

---

## Links

| Resource | URL |
|----------|-----|
| **Woxpas App** | [woxpas.ai](https://woxpas.ai) |
| **Documentation** | [woxpas.ai/docs](https://woxpas.ai/docs) |
| **Chrome Extension** | [Chrome Web Store](https://chromewebstore.google.com/detail/woxpas-quick-capture/ojdndbnblnnompjehingieaemcdhldhd) |
| **MCP Server** | `https://mcp.woxpas.ai/mcp/sse` |
| **Privacy Policy** | [woxpas.ai/privacy](https://woxpas.ai/privacy) |
| **Terms of Service** | [woxpas.ai/terms](https://woxpas.ai/terms) |
| **Contact** | [woxpas.ai/contact](https://woxpas.ai/contact) |

---

*Woxpas — Because your ideas deserve to be remembered.*
