# Drakyn AI Agent Context

This file is automatically loaded by Claude Code at the start of every session.

## User Information

**Name**: Chanh

**Session Greeting Protocol**: At the start of every new chat session:
1. Greet Chanh by name
2. Confirm that you've loaded the memory system
3. Identify which machine you're on (Windows WSL or Ubuntu server)

This lets him know you have context from previous sessions and are aware of the environment.

## Memory System

Your persistent memory is stored in this repository under `memory/`:
- **Session Log**: `memory/logs/session-log.md` - Detailed history of past work
- **Current Projects**: `memory/context/current-projects.md` - Active project tracking

At the start of each session, you should be aware of the memory system and can reference these files when context is needed.

## Environment

This configuration is shared across multiple machines:

### Windows Development Machine (WSL)
- **Location**: `/mnt/c/Users/chanh/drakyn`
- **Purpose**: Primary development for drakyn-desktop (has local GPU)
- **OS**: Windows with WSL2 (Ubuntu)
- **Tools Available**: git, standard Linux tools in WSL

### Ubuntu Web Server
- **Location**: `/home/cnguyen`
- **Public IP**: 20.59.111.132
- **Purpose**: Production hosting for web applications (drakyn-agent)
- **OS**: Ubuntu Linux
- **Tools Available**: gh CLI, git, standard Linux tools, nginx, systemd

### Shared Configuration
- **GitHub User**: chanh
- **Organization**: drakyn-ai (use for all repositories)
- **Repo Sync**: Same agent-config repo used on both machines for consistent preferences and shared memory

## Global Configuration

Configuration is symlinked globally:
- `~/.claude/commands` → `~/agent-config/.claude/commands`
- `~/.claude/settings.json` → `~/agent-config/.claude/settings.json`
- `~/memory` → `~/agent-config/memory`

Custom slash commands available: `/remember`, `/recall`, `/memory-sync`

## Active Projects

See `memory/context/current-projects.md` for current status of:
- **agent-config**: This repository (configuration management)
- **drakyn-agent**: AI assistant web app at agent.drakyn.ai (Ubuntu server)
- **drakyn-desktop**: Desktop AI application with local GPU support (Windows development machine)

## Preferences

- Use conventional commits for git messages
- Create all repos under drakyn-ai organization
- Default branch: main
- Code style: TypeScript preferred, 2 spaces, semicolons
- Update memory files at significant milestones
- Auto-commit memory changes to preserve context

## Custom Commands

- `/remember <content>` - Add important information to memory
- `/recall [query]` - Search and retrieve from memory
- `/memory-sync` - Commit memory changes to git
