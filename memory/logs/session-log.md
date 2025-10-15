# Claude Code Session Log

This file maintains a curated log of important information, decisions, and context across sessions.

## Purpose
This log serves as long-term memory, allowing Claude to:
- Remember important facts about projects and preferences
- Track decisions and their rationale
- Maintain context about ongoing work
- Learn from past interactions

## How It Works
- Claude reads this file at the start of sessions to recall context
- Claude updates this file with important learnings and decisions
- Changes are committed to git for version history
- Entries are curated to keep only relevant information

---

## Session History

### 2025-10-15 - Initial Setup

**Environment Setup:**
- Server: Linux server with public-facing IP at /home/cnguyen
- GitHub: Authenticated with gh CLI under user 'chanh'
- Organization: drakyn-ai (for all repo creation)

**Repositories Created:**
- `drakyn-ai/agent-config` - Configuration and memory repository for Claude Code
  - Location: ~/agent-config
  - Purpose: Store preferences, custom commands, prompts, and session memory
  - Git configured with gh credential helper for authentication

**Key Preferences:**
- All repositories should be created under drakyn-ai organization
- Using conventional commits for git messages
- Default branch: main

**Memory System Established:**
- Memory stored in this repo under memory/logs/
- Session context in memory/context/
- Claude maintains and curates this log across sessions
- Regular commits to preserve knowledge

**Global Configuration Setup:**
- Symlinked `~/.claude/commands` → `~/agent-config/.claude/commands`
- Symlinked `~/.claude/settings.json` → `~/agent-config/.claude/settings.json`
- Symlinked `~/memory` → `~/agent-config/memory`
- Preserved existing `~/.claude/settings.local.json` with permissions
- Configuration now loads automatically in every session regardless of working directory

**User Workflow:**
- Uses VSCode connected to VM
- Claude Code in right-hand panel
- All sessions now have access to custom commands (/remember, /recall, /memory-sync, /example)
- Memory system accessible globally via ~/memory

---

### 2025-10-15 - Drakyn Agent Project

**Project Created: Drakyn Agent**
- Repository: `drakyn-ai/drakyn-agent`
- Location: ~/drakyn-agent
- Domain: agent.drakyn.ai (DNS to be configured by user)
- Purpose: 24/7 AI assistant accessible via secure web interface

**Technical Stack:**
- Backend: FastAPI (Python) with Uvicorn
- Frontend: HTML/CSS/JavaScript with WebSockets
- AI: Anthropic Claude API with streaming responses
- Authentication: Google OAuth 2.0
- Database: SQLite for conversation persistence
- Web Server: Nginx reverse proxy
- SSL: Let's Encrypt (Certbot)
- Service: systemd for 24/7 operation

**Security Features:**
- Google OAuth 2.0 authentication
- Email-based access control (ALLOWED_EMAIL)
- HTTPS enforced via Let's Encrypt
- JWT token-based sessions
- HTTP-only secure cookies
- Security headers configured in Nginx
- WebSocket authentication

**Key Features Implemented:**
- Real-time chat with streaming responses via WebSocket
- Conversation history with SQLite persistence
- Multiple conversation support
- Modern, responsive dark-themed UI
- Automatic SSL setup
- Complete setup automation script
- Health check endpoints

**Server Configuration:**
- Public IP: 20.59.111.132
- Internal Port: 8000 (Uvicorn)
- External Port: 443 (Nginx HTTPS)
- DNS: agent.drakyn.ai → 20.59.111.132

**User Action Items:**
1. Configure DNS A record: agent → 20.59.111.132 at name.com
2. Set up Google OAuth credentials at console.cloud.google.com
3. Get Anthropic API key from console.anthropic.com
4. Configure .env file with credentials
5. Run ./setup.sh to complete installation

**Files Created:**
- Complete FastAPI application with auth, database, Claude integration
- WebSocket chat implementation with streaming
- Modern chat UI with conversation management
- Nginx configuration with SSL support
- Systemd service file
- Automated setup script
- Comprehensive documentation (README.md, QUICKSTART.md)

**Future Enhancement Ideas:**
- Tool use and code execution capabilities
- Web search integration
- File upload/download
- Multi-user support
- Custom system prompts per conversation
- Model selection (different Claude variants, other providers)
- Voice input/output
- Mobile app

**Next Steps:**
- User to configure DNS and credentials
- Run setup script for deployment
- Test authentication and chat functionality
- Monitor service and iterate on features
