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

**Implementation Complete (2025-10-17):**
1. ✅ Architecture design committed to memory
2. ✅ Implemented agent/orchestrator.py (285 lines - core reasoning loop)
3. ✅ Implemented agent/models.py (89 lines - Pydantic schemas)
4. ✅ Implemented agent/prompts.py (77 lines - system prompts)
5. ✅ Updated server.py with /v1/agent/chat endpoint (SSE streaming)
6. ✅ Implemented FileSearchTool (131 lines - file search with wildcards)
7. ✅ Updated UI to display agent steps in real-time
8. ✅ Enabled MCP server in Electron main.js
9. ✅ Created comprehensive AGENT_ARCHITECTURE.md documentation
10. ✅ Committed and pushed to GitHub

**Total Implementation:**
- 14 files modified/created
- ~1,459 lines added
- Complete agent architecture operational
- Ready for testing with local vLLM models

**Components Implemented:**
- AgentOrchestrator with streaming support
- LiteLLMClient for multi-provider LLM access
- Type-safe Pydantic models throughout
- MCP tool server with registry pattern
- FileSearchTool (supports wildcards, recursive search)
- SSE streaming from server to UI
- Real-time agent reasoning visualization

**Recent Updates (2025-10-20):**

**Proactive Agent Design:**
- ✅ Designed proactive agent architecture (background monitoring, suggestions, learning)
- ✅ Created detailed architecture document: `docs/PROACTIVE_AGENT.md`
- ✅ Key insight: Use plain text memory instead of SQLite database
- ✅ Agent manages its own memory in `~/.drakyn/user_context.txt`
- ✅ Implemented `user_context` tool (read/update plain text memory)
- ✅ Tool registered in MCP server

**Proactive Agent Vision:**
Transform from reactive chat agent into proactive, context-aware assistant that:
- Monitors user context (emails, calendar, system state) in background
- Proactively suggests helpful actions based on learned context
- Asks questions to learn about user's life, preferences, patterns
- Manages its own memory in natural language (plain text file)

**Architecture Components:**
1. **User Context System** (`~/.drakyn/user_context.txt`)
   - Plain text memory managed by agent
   - Natural language, human-readable
   - Agent reads/updates using `user_context` tool

2. **Background Monitor Service** (to be implemented)
   - Runs every 30-60 minutes
   - Gathers context snapshots (emails, calendar, system)
   - Calls agent to analyze and suggest actions

3. **Context Analyzer** (to be implemented)
   - LLM-based analysis of current situation
   - Generates proactive suggestions
   - Respects user preferences

4. **Learning System** (to be implemented)
   - Asks questions to build user context
   - Agent updates its own context file
   - Max 3 questions per day

5. **Notification System** (to be implemented)
   - System notifications
   - In-app suggestion panel
   - Respects quiet hours

**Design Philosophy:**
- **Plain text over database:** LLMs work best with natural language
- **Agent self-manages:** Agent reads/writes its own memory
- **Privacy-first:** All data local, human-readable, easy to delete
- **Simple implementation:** ~500 lines of code vs 2000+ with database

**Implementation Status (✅ ALL PHASES COMPLETE - PRODUCTION READY):**
- ✅ Design complete (docs/PROACTIVE_AGENT.md)
- ✅ user_context tool implemented and registered
- ✅ Background monitor service implemented (src/services/monitor/service.py)
- ✅ Context analyzer with LLM-based suggestions
- ✅ Electron integration (auto-start background process)
- ✅ Email monitoring via Gmail tool
- ✅ System state monitoring (battery, etc.)
- ✅ Quiet hours support
- ✅ Suggestion logging and history
- ✅ Notification system (IPC server, system notifications, in-app panel)
- ✅ User interaction (accept/dismiss buttons)
- ✅ Real-time suggestion updates via IPC
- ✅ Learning system (proactive questions, context updates)
- ✅ Settings UI for preferences (complete configuration)
- ⚠️ Calendar integration (placeholder tool, full OAuth pending)

**🎉 Complete Feature Set:**

1. **Background Monitoring**
   - Runs every 30 minutes (configurable: 15/30/60/120)
   - Gathers context from Gmail and system state
   - Respects quiet hours (configurable in Settings)
   - Enable/disable via Settings UI

2. **Intelligent Suggestions**
   - LLM analyzes context holistically
   - Only suggests when truly helpful
   - Considers user preferences and patterns
   - All suggestions logged with reasoning

3. **Notification System**
   - System notifications (native OS)
   - In-app floating panel with modern UI
   - Badge showing pending count
   - Accept/dismiss with visual feedback

4. **Learning System**
   - Asks up to 3 questions per day (configurable)
   - Questions every 3rd check (~90 minutes)
   - Agent updates user context via tool
   - Learns preferences naturally

5. **User Context**
   - Plain text at ~/.drakyn/user_context.txt
   - Agent reads and updates naturally
   - Human-readable and editable
   - Privacy-first (all local)

6. **Settings UI**
   - Complete proactive agent configuration
   - All preferences configurable
   - Settings persist across restarts
   - Helpful explanations included

**Architecture:**
```
Monitor Service (Python) → IPC Server (Node.js:9999)
                              ↓
                    System Notification (Electron)
                              ↓
                    Renderer Process (IPC event)
                              ↓
                    Suggestion Panel (React-like UI)
                              ↓
                    User Action (Accept/Dismiss)
```

**Files & Stats:**
- Total implementation: ~2,500 lines across 4 phases
- Time invested: ~4 hours
- 8 major components fully implemented
- Comprehensive testing guide created
- Production-ready documentation

**Testing:**
- See docs/PROACTIVE_AGENT_TESTING.md
- Quick test: `curl -X POST http://localhost:9999/notify ...`
- Recommended: 2-minute interval for testing, 30-60 for production

**Next Steps (Future Enhancements):**
1. Full Google Calendar integration (OAuth + API)
2. Learning question answer processing in UI
3. Suggestion effectiveness analytics
4. Conversation context linking
5. Multi-account support
6. Mobile companion app

---

## Project Ideas / Backlog

- DNS management automation (name.com API integration)
- Infrastructure monitoring dashboard
- Automated backup system
- CI/CD pipeline for projects

---

## Completed Projects

(Completed projects will be moved here for reference)
