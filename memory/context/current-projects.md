# Current Projects and Active Work

This file tracks ongoing projects, their status, and next actions.

## Active Projects

### agent-config Repository
**Status:** Complete (Ongoing Maintenance)
**Location:** ~/agent-config
**Repository:** drakyn-ai/agent-config

**Description:**
Configuration and memory management system for Claude Code and other AI coding agents.

**Features:**
- Claude Code settings and preferences
- Custom slash commands (/remember, /recall, /memory-sync)
- Prompt templates
- Memory/logging system for long-term context
- Global symlinks for automatic discovery

**Next Steps:**
- Add more custom commands as workflows develop
- Maintain memory logs across sessions

---

### Drakyn Agent
**Status:** Development (Ready for Deployment with Gmail Integration)
**Location:** ~/drakyn-agent
**Repository:** drakyn-ai/drakyn-agent
**Domain:** agent.drakyn.ai

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

## Project Ideas / Backlog

- DNS management automation (name.com API integration)
- Infrastructure monitoring dashboard
- Automated backup system
- CI/CD pipeline for projects

---

## Completed Projects

(Completed projects will be moved here for reference)
