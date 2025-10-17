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
**Status:** Planning / Initial Development
**Location:** Windows: `/mnt/c/Users/chanh/drakyn/drakyn-desktop`
**Repository:** drakyn-ai/drakyn-desktop (to be created)
**Machine:** Windows development machine with WSL

**Description:**
Desktop AI application with local GPU support for enhanced performance and capabilities.

**Key Advantages:**
- Local GPU acceleration for faster inference
- Offline capabilities
- Direct system integration
- Privacy-focused (local processing)

**Planned Features:**
- Local LLM inference with GPU acceleration
- Desktop integration (file system, clipboard, etc.)
- Voice input/output
- Screen capture and analysis
- Code execution environment
- Cross-platform support (Windows, Linux, macOS)

**Tech Stack (Proposed):**
- Electron or Tauri for desktop framework
- Python backend for AI/ML processing
- Local model inference (Llama, Mistral, or similar)
- GPU acceleration (CUDA, ROCm)
- TypeScript/React for UI

**Current Status:**
- Project in planning phase
- Development to occur on Windows machine (has local GPU)
- Repo not yet created

**Next Steps:**
1. Define core features and architecture
2. Choose desktop framework (Electron vs Tauri)
3. Select local LLM solution
4. Create repository structure
5. Begin initial implementation

---

## Project Ideas / Backlog

- DNS management automation (name.com API integration)
- Infrastructure monitoring dashboard
- Automated backup system
- CI/CD pipeline for projects

---

## Completed Projects

(Completed projects will be moved here for reference)
