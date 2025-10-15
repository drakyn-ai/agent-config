# Memory System Documentation

## Overview

This memory system provides Claude Code with long-term context across sessions by maintaining curated logs in the git repository.

## How It Works

1. **Session Logs** - Main memory file tracking important information
2. **Context Files** - Specific context about projects, preferences, decisions
3. **Git History** - Version control provides timeline and audit trail
4. **Curation** - Claude maintains and updates logs, keeping only relevant info

## File Structure

```
memory/
├── logs/
│   └── session-log.md          # Main chronological log
└── context/
    ├── current-projects.md      # Active projects and status
    ├── preferences.md           # User preferences and patterns
    └── decisions.md             # Important decisions and rationale
```

## What Gets Logged

### Always Log:
- New projects and repositories created
- Important technical decisions and why they were made
- Server configuration changes
- New tools or services deployed
- User preferences and workflow patterns
- Lessons learned from debugging or problem-solving

### Sometimes Log:
- Significant features or changes to projects
- Useful code patterns or techniques discovered
- External service configurations (APIs, webhooks, etc.)

### Don't Log:
- Routine tasks or trivial changes
- Temporary debugging information
- Sensitive data (passwords, API keys, etc.)
- Excessive detail about common operations

## Memory Workflow

### At Session Start:
1. Claude reads session-log.md and relevant context files
2. Recalls previous work, preferences, and decisions
3. Understands current state of projects

### During Session:
1. Claude notes important information internally
2. At natural breakpoints, updates relevant memory files
3. Commits changes with descriptive messages

### At Session End (if significant work done):
1. Claude curates session log with key learnings
2. Updates project status in context files
3. Commits and pushes memory updates

## Using the Memory System

### For Users:
- Read session-log.md to see what Claude remembers
- Add your own notes or corrections to context files
- Review memory commits to see what's being tracked
- Ask Claude to remember specific things: "Remember that I prefer X"

### For Claude:
- Read memory files at session start
- Update memory when learning important information
- Keep entries concise and well-organized
- Use conventional commit messages for memory updates
- Prune outdated information periodically

## Custom Commands

Use `/remember [topic]` to explicitly ask Claude to log something to memory.
Use `/recall [topic]` to ask Claude to check memory for specific information.

## Benefits

- **Continuity**: Pick up where you left off
- **Context**: Claude understands project history
- **Learning**: Avoid repeating past mistakes
- **Preferences**: Remember how you like things done
- **Collaboration**: Share context with other agents or developers

## Privacy Note

All memory is stored in git and pushed to GitHub. Don't log sensitive information.
