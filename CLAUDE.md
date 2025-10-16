# Drakyn AI Agent Context

This file is automatically loaded by Claude Code at the start of every session.

## Memory System

Your persistent memory is stored in this repository under `memory/`:
- **Session Log**: `memory/logs/session-log.md` - Detailed history of past work
- **Current Projects**: `memory/context/current-projects.md` - Active project tracking

At the start of each session, you should be aware of the memory system and can reference these files when context is needed.

## Environment

- **Server**: Linux VM at /home/cnguyen with public IP (20.59.111.132)
- **GitHub User**: chanh
- **Organization**: drakyn-ai (use for all repositories)
- **Tools Available**: gh CLI, git, standard Linux tools

## Global Configuration

Configuration is symlinked globally:
- `~/.claude/commands` → `~/agent-config/.claude/commands`
- `~/.claude/settings.json` → `~/agent-config/.claude/settings.json`
- `~/memory` → `~/agent-config/memory`

Custom slash commands available: `/remember`, `/recall`, `/memory-sync`

## Active Projects

See `memory/context/current-projects.md` for current status of:
- **agent-config**: This repository (configuration management)
- **drakyn-agent**: AI assistant web app at agent.drakyn.ai

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
