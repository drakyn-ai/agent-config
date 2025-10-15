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

**Next Steps:**
- Continue building cool projects on this server
- Utilize the memory system for long-term context
- Expand custom commands as workflows develop
