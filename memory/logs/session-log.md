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

**User Information:**
- Name: Chanh
- Username: cnguyen / chanh (GitHub)

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

---

### 2025-10-16 - Automatic Memory Loading

**Enhancement: CLAUDE.md Auto-Loading**
- Created `CLAUDE.md` in agent-config repository
- File automatically loads at start of every Claude Code session
- Provides immediate context about memory system, preferences, and active projects
- Symlinked to `~/.claude/CLAUDE.md` for global availability

**How It Works:**
- Claude Code automatically reads CLAUDE.md files at session start
- Loads recursively from current directory up to home directory
- Symlink ensures it's always available regardless of working directory
- Eliminates need to manually check memory at session start

**Benefits:**
- Claude has context from the very beginning of each session
- User doesn't need to prompt for memory recall
- Seamless continuity across sessions
- Can still use `/recall` for deep dives into specific past work

**Session Greeting Protocol:**
- Added user name (Chanh) to CLAUDE.md
- Claude will greet Chanh by name at the start of each session
- Confirms memory initialization so user knows context is loaded

---

### 2025-10-16 - Drakyn Agent Architecture Deep Dive

**Completed Full Codebase Exploration**

Conducted comprehensive analysis of drakyn-agent architecture and committed detailed understanding to memory.

**Architecture Overview:**
- **Type:** 24/7 AI assistant web application
- **Core Technology:** FastAPI backend + vanilla JavaScript frontend
- **AI Integration:** Anthropic Claude API with WebSocket streaming
- **Authentication:** Google OAuth 2.0 with JWT tokens
- **Data Persistence:** SQLite database for conversations and messages

**Project Structure:**
```
drakyn-agent/
├── app/                        # Main application code
│   ├── main.py                # FastAPI routes & WebSocket
│   ├── config.py              # Environment configuration
│   ├── auth.py                # JWT & OAuth utilities
│   ├── claude_client.py       # Anthropic API client
│   ├── database.py            # SQLite operations
│   ├── templates/             # Jinja2 HTML templates
│   │   ├── login.html        # OAuth login page
│   │   └── chat.html         # Chat interface
│   └── static/                # Frontend assets
│       ├── js/chat.js        # WebSocket chat logic
│       └── css/style.css     # UI styling
├── data/                      # Runtime data
│   └── conversations.db      # SQLite database
├── nginx.conf                 # Reverse proxy config
├── drakyn-agent.service       # Systemd service
└── setup.sh                   # Automated deployment
```

**Key Components:**

1. **main.py** - Application Core
   - Routes: /, /login, /auth/callback, /logout, /chat
   - API endpoints: /api/conversations (GET/POST), /api/conversations/{id}
   - WebSocket: /ws/chat/{conversation_id} for streaming
   - SessionMiddleware for session management
   - Health check endpoint at /health

2. **auth.py** - Authentication System
   - `create_access_token()` - Generate JWT (7-day expiry)
   - `verify_token()` - Validate JWT signatures
   - `get_current_user()` - Extract user from Bearer token
   - `get_user_from_cookie()` - Cookie-based auth
   - Email whitelist enforcement (ALLOWED_EMAIL)

3. **claude_client.py** - AI Integration
   - `stream_claude_response()` - AsyncGenerator for streaming
   - `get_claude_response()` - Complete response retrieval
   - Configurable model selection (default: claude-sonnet-4-5-20250929)
   - System prompt customization
   - Max tokens: 4096 default

4. **database.py** - Data Layer
   - Async SQLite operations via aiosqlite
   - Tables: conversations (metadata), messages (content)
   - Functions: create_conversation, add_message, get_conversation_messages, get_user_conversations, delete_conversation
   - Row-level security: conversations tied to user_email

5. **chat.js** - Frontend Logic
   - WebSocket connection with token authentication
   - Real-time message streaming with chunk display
   - Conversation management (create, switch, load history)
   - Model selection dropdown (7 Claude models)
   - Auto-scroll and typing indicators

**Application Flows:**

**Authentication Flow:**
```
Visit agent.drakyn.ai
  → GET / (redirects to login if not authenticated)
  → GET /login (OAuth redirect to Google)
  → User authorizes
  → GET /auth/callback (receives token, validates email)
  → create_access_token() generates JWT
  → Sets cookies: access_token (HttpOnly), ws_token (JS-readable)
  → Redirect to /chat
```

**Message Streaming Flow:**
```
WebSocket connection to /ws/chat/{conversation_id}
  → Send token for authentication
  → User sends message + model selection
  → Validate token, save user message to DB
  → Load conversation history from DB
  → Call Claude API with stream_claude_response()
  → Stream chunks: {"type": "chunk", "content": text}
  → Frontend appends chunks in real-time
  → Send {"type": "end"} when complete
  → Save assistant message to DB
  → Re-enable input field
```

**Security Model:**
- Google OAuth 2.0 as single entry point
- Email whitelist (ALLOWED_EMAIL environment variable)
- JWT tokens with 7-day expiration
- HTTP-only cookies for regular auth
- HTTPS enforced via Nginx + Let's Encrypt
- HSTS, X-Frame-Options, X-Content-Type-Options headers
- SameSite=lax for CSRF protection
- User cannot access others' conversations (DB-level verification)

**Deployment Architecture:**
- Uvicorn serves FastAPI on 127.0.0.1:8000
- Nginx reverse proxy on port 443 (HTTPS)
- WebSocket upgrade support with 86400s timeout
- Systemd service for auto-restart and logging
- Let's Encrypt for SSL certificates

**Available Models:**
7 Claude variants selectable in chat interface:
- claude-sonnet-4-5-20250929 (default)
- claude-opus-4-20250514
- claude-sonnet-3-7-20250219
- claude-3-5-sonnet-20241022
- claude-3-5-haiku-20241022
- claude-3-opus-20240229
- claude-3-haiku-20240307

**Database Schema:**
- **conversations**: id, user_email, title, created_at, updated_at
- **messages**: id, conversation_id, role (user/assistant), content, timestamp

**Dependencies:**
- Web: fastapi, uvicorn[standard], starlette
- AI: anthropic
- Auth: authlib, python-jose[cryptography]
- DB: aiosqlite
- WebSocket: websockets
- Templating: jinja2
- Utils: python-multipart, python-dotenv, httpx, itsdangerous

**Future Enhancements Planned:**
- Tool use and code execution
- Web search integration
- File upload/download
- Multi-user support (remove email whitelist)
- Custom system prompts per conversation
- Voice input/output
- Mobile application

**Current Status:**
- Codebase complete and pushed to GitHub
- Awaiting: DNS configuration, Google OAuth credentials, Anthropic API key
- Ready for deployment via ./setup.sh once credentials are configured

---

### 2025-10-16 - Gmail Integration Implementation

**Feature: Gmail Integration with Claude Tool Use**

Successfully implemented comprehensive Gmail integration allowing Claude to access and interact with the user's Gmail inbox through tool use.

**Implementation Details:**

1. **OAuth Scope Update** ([main.py:33-43](drakyn-agent/app/main.py#L33-L43))
   - Added `https://www.googleapis.com/auth/gmail.readonly` scope
   - Set `access_type: 'offline'` to get refresh token
   - Set `prompt: 'consent'` to force consent screen

2. **OAuth Token Storage** ([database.py:36-47](drakyn-agent/app/database.py#L36-L47))
   - Created `oauth_tokens` table with fields:
     - user_email (unique), access_token, refresh_token, token_type, expires_at
   - Added `store_oauth_token()` function with upsert logic
   - Added `get_oauth_token()` function for retrieval
   - Tokens stored per-user in database

3. **Gmail Client Module** ([gmail_client.py](drakyn-agent/app/gmail_client.py))
   - Created async Gmail API wrapper
   - Implemented 4 main functions:
     - `list_emails()` - List recent emails with optional query filter
     - `read_email()` - Read full email content by message ID
     - `search_emails()` - Search using Gmail syntax
     - `get_recent_unread_emails()` - Quick shortcut for unread
   - Handles OAuth credentials with refresh token support
   - Extracts email metadata (from, to, subject, date, snippet)
   - Decodes base64 email body content

4. **Claude Tool Use Integration** ([claude_client.py:10-189](drakyn-agent/app/claude_client.py#L10-L189))
   - Defined 4 Gmail tools with detailed schemas:
     - `list_emails` - Max 50 results, optional query
     - `read_email` - Requires message_id
     - `search_emails` - Requires query, supports Gmail operators
     - `get_recent_unread_emails` - Max 20 results
   - Enhanced `stream_claude_response()` with:
     - Tool definitions passed to Claude API
     - Automatic tool execution when Claude requests
     - Tool result handling and conversation continuation
     - Support for multiple tool use rounds
   - Updated system prompt to mention Gmail access

5. **WebSocket Integration** ([main.py:224](drakyn-agent/app/main.py#L224))
   - Pass `user_email` to Claude streaming function
   - Enables per-user OAuth token retrieval
   - Maintains security isolation between users

6. **Dependencies Added** ([requirements.txt:15-18](drakyn-agent/requirements.txt#L15-L18))
   - google-api-python-client==2.111.0
   - google-auth==2.26.2
   - google-auth-oauthlib==1.2.0
   - google-auth-httplib2==0.2.0

**Gmail Tool Capabilities:**

**Supported Search Operators:**
- `from:email@example.com` - Filter by sender
- `to:email@example.com` - Filter by recipient
- `subject:keyword` - Search subject line
- `is:unread` - Only unread emails
- `is:starred` - Only starred emails
- `has:attachment` - Has attachments
- `after:2024/1/1` - After specific date
- `before:2024/12/31` - Before specific date
- `newer_than:7d` - Last N days
- `older_than:30d` - Older than N days

**Example User Queries:**
- "Show me my 5 most recent emails"
- "Find emails from john@company.com about the project"
- "Do I have any unread emails?"
- "Search for emails with attachments from last week"
- "Read the full content of email [message_id]"

**Security & Privacy:**
- Read-only Gmail access (cannot send or delete)
- OAuth tokens stored per-user, encrypted in database
- Refresh tokens preserved for long-term access
- User must re-authenticate if tokens expire or are revoked
- Each user can only access their own emails (DB-level isolation)

**Architecture Flow:**
```
User asks about emails
  → Claude decides to use Gmail tool
  → Tool execution retrieves OAuth token from DB
  → Gmail API called with user's credentials
  → Results returned to Claude
  → Claude streams response with email information
  → User sees natural language summary
```

**Testing Status:**
- Code implementation complete
- Awaiting deployment to test with real Gmail account
- Need to enable Gmail API in Google Cloud Console
- OAuth consent screen must include Gmail readonly scope

**Next Steps for Deployment:**
1. Enable Gmail API in Google Cloud Console
2. Update OAuth consent screen with Gmail scope
3. Deploy to production server
4. Test authentication flow with Gmail consent
5. Verify tool execution and email access
6. Monitor API quota and error handling

**Future Enhancements:**
- Gmail send/compose capabilities (requires different scope)
- Email draft management
- Label/folder organization
- Mark as read/unread
- Star/unstar emails
- Archive/trash operations (requires modify scope)
