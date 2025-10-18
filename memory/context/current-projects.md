# Current Projects and Active Work

This file tracks ongoing projects, their status, and next actions.

## Active Projects

### agent-config Repository
**Status:** Complete (Ongoing Maintenance)
**Location:**
- Windows: `/mnt/c/Users/chanh/drakyn/agent-config`
- Ubuntu Server: `~/agent-config`
**Repository:** drakyn-ai/agent-config

**Description:**
Configuration and memory management system for Claude Code and other AI coding agents. Shared across both Windows development machine and Ubuntu web server.

**Features:**
- Claude Code settings and preferences
- Custom slash commands (/remember, /recall, /memory-sync)
- Prompt templates
- Memory/logging system for long-term context
- Global symlinks for automatic discovery
- Multi-machine support with git sync

**Next Steps:**
- Add more custom commands as workflows develop
- Maintain memory logs across sessions
- Keep synced between machines via git

---

### Drakyn Agent (Web Application)
**Status:** Development (Ready for Deployment with Gmail Integration)
**Location:** Ubuntu Server: `~/drakyn-agent`
**Repository:** drakyn-ai/drakyn-agent
**Domain:** agent.drakyn.ai
**Machine:** Ubuntu web server (20.59.111.132)

**Description:**
24/7 AI assistant powered by Claude, accessible via secure web interface with Google OAuth authentication and Gmail integration.

**Tech Stack:**
- FastAPI + Uvicorn + Nginx
- Google OAuth 2.0 with Gmail API
- Anthropic Claude API with Tool Use
- SQLite database
- WebSocket streaming
- Let's Encrypt SSL
- Systemd service

**Current Features:**
- ✅ Complete codebase implemented
- ✅ Gmail integration with Claude tool use
- ✅ Real-time email access (list, search, read)
- ✅ OAuth token storage and management
- ✅ Pushed to GitHub
- ⏳ Awaiting DNS configuration
- ⏳ Awaiting OAuth credentials setup (needs Gmail API enabled)
- ⏳ Awaiting Anthropic API key
- ⏳ Ready for ./setup.sh deployment

**Gmail Integration:**
- Read-only access to user's Gmail
- 4 tools: list_emails, read_email, search_emails, get_recent_unread_emails
- Full Gmail search syntax support (from:, subject:, is:unread, etc.)
- Secure OAuth token storage per-user
- Automatic tool execution during Claude conversations

**Next Steps:**
1. User configures DNS at name.com
2. User sets up Google OAuth + enables Gmail API
3. User gets Anthropic API key
4. User runs ./setup.sh
5. Test Gmail integration end-to-end
6. Monitor and iterate on features

**Future Enhancements:**
- Gmail send/compose capabilities
- Google Calendar integration
- Google Drive integration
- Web search integration
- Code execution
- File upload/download
- Multi-user support
- Custom system prompts
- Voice I/O

---

### Drakyn Desktop (Desktop Application)
**Status:** Active Development - Agent Architecture Implementation
**Location:** Windows: `/mnt/c/Users/chanh/drakyn/drakyn-desktop`
**Repository:** drakyn-ai/drakyn-desktop
**Machine:** Windows development machine with WSL (local GPU)

**Description:**
Desktop AI agent application with local GPU inference and tool integration via Model Context Protocol (MCP).

**Key Advantages:**
- Local GPU acceleration for faster inference
- Offline-capable agent with tool execution
- Direct system integration (email, files, code execution)
- Privacy-focused (local processing)
- Hybrid architecture: custom orchestration + off-the-shelf components

**Current Tech Stack:**
- **Desktop Framework:** Electron
- **Backend:** Python 3 with FastAPI
- **Inference Engine:** vLLM (local GPU acceleration)
- **Agent Framework:** Custom orchestration loop
- **Tool Protocol:** MCP (Model Context Protocol)
- **LLM Abstraction:** LiteLLM (multi-provider support)
- **Structured Outputs:** Instructor (Pydantic-based parsing)
- **UI:** Vanilla JavaScript with dark VS Code theme
- **GPU:** CUDA support via vLLM

**Architecture Decision (2025-10-17):**
After evaluating LangChain vs LangGraph vs custom implementation, chose **hybrid approach**:
- **Custom agent orchestrator** - Simple, transparent reasoning loop (~300 lines)
- **LiteLLM** - Multi-provider LLM calls (OpenAI, Anthropic, local vLLM)
- **Instructor** - Reliable structured output parsing (tool calls)
- **MCP SDK** - Standard tool protocol for extensibility

**Rationale:**
- Speed: Direct control over reasoning flow, no graph abstractions
- Context size: Small focused modules (~100-250 lines each) for coding agent modifications
- Flexibility: Use off-the-shelf components where they add value, custom code for core logic
- Debuggability: Linear execution, transparent flow, standard Python debugging

**Current Implementation Status:**
- ✅ Electron app with VS Code dark theme UI
- ✅ vLLM inference server with auto-setup
- ✅ Python virtualenv management (reuses after first run)
- ✅ Model loading/unloading via UI
- ✅ Basic chat interface with streaming
- ✅ Connection status monitoring
- ⏳ Agent orchestrator (in progress)
- ⏳ Tool calling support
- ⏳ MCP tool implementations (email, files, code)
- ⏳ Streaming agent thinking steps to UI

**File Structure:**
```
src/
├── electron/
│   ├── main.js              # Electron lifecycle, service spawning
│   └── preload.js           # Security bridge
├── services/
│   ├── inference/
│   │   ├── server.py        # FastAPI + vLLM
│   │   ├── agent/           # NEW: Agent components
│   │   │   ├── orchestrator.py  # Core reasoning loop
│   │   │   ├── models.py        # Pydantic schemas
│   │   │   └── prompts.py       # System prompts
│   │   ├── providers/       # NEW: LLM abstraction
│   │   │   └── litellm_client.py
│   │   ├── setup.js         # Python env initialization
│   │   └── requirements.txt
│   └── mcp/
│       ├── server.py        # Tool registry & execution
│       ├── tools/           # NEW: Tool implementations
│       │   ├── email.py
│       │   ├── files.py
│       │   └── code.py
│       └── requirements.txt
└── public/
    ├── index.html           # Chat UI
    ├── app.js               # Frontend logic
    └── styles.css           # Dark theme
```

**Agent Flow (Example: "Read my latest emails"):**
```
User message
  → AgentOrchestrator.run()
    → LiteLLM.completion() with tools schema
    → Instructor.parse() extracts tool call
    → MCP client executes tool via HTTP
    → Tool result added to context
    → LiteLLM generates final answer
    → Stream steps to UI
```

**Dependencies:**
```
Inference server:
- vllm>=0.3.0          # GPU inference
- litellm>=1.0.0       # Multi-provider
- instructor>=1.0.0    # Structured outputs
- mcp>=1.0.0           # Tool protocol
- fastapi, uvicorn, torch, pydantic

MCP server:
- mcp>=1.0.0
- fastapi, uvicorn, pydantic
```

**Current Session Tasks:**
1. ✅ Architecture design committed to memory
2. ⏳ Implement agent/orchestrator.py (core reasoning loop)
3. ⏳ Implement agent/models.py (Pydantic schemas)
4. ⏳ Implement agent/prompts.py (system prompts)
5. ⏳ Update server.py with /v1/agent/chat endpoint
6. ⏳ Implement example MCP tool (email)
7. ⏳ Update UI to display agent steps

**Next Steps:**
1. Complete agent orchestrator implementation
2. Test tool calling with local vLLM model
3. Implement email tool (IMAP/Gmail API)
4. Add file search tool
5. Add code execution tool (sandboxed)
6. Build streaming UI for agent reasoning steps
7. Test end-to-end agent flow

---

## Project Ideas / Backlog

- DNS management automation (name.com API integration)
- Infrastructure monitoring dashboard
- Automated backup system
- CI/CD pipeline for projects

---

## Completed Projects

(Completed projects will be moved here for reference)
