# Agent Configuration

This repository contains configuration files and preferences for working with AI coding agents, including Claude Code and other tools.

## Purpose

This repo serves as a centralized location for:
- Claude Code configurations and custom commands
- Shared preferences across different coding agents
- Common prompts and workflows
- Documentation for agent interactions

## Structure

```
agent-config/
├── .claude/              # Claude Code specific configurations
│   ├── commands/         # Custom slash commands
│   └── settings.json     # Claude Code settings
├── memory/               # Long-term memory system
│   ├── logs/            # Session logs and history
│   └── context/         # Project and preference context
├── prompts/              # Reusable prompts and templates
└── docs/                 # Documentation and guides
```

## Getting Started

### Claude Code Configuration

The `.claude` directory contains Claude Code specific configurations:

- **Custom Commands**: Add custom slash commands in `.claude/commands/`
- **Settings**: Configure Claude Code behavior in `.claude/settings.json`

### Memory System

The memory system provides Claude Code with long-term context across sessions:

- **Session Logs**: Track important decisions, learnings, and project history
- **Context Files**: Maintain current state of projects and preferences
- **Git History**: Version control provides audit trail of memory evolution

Custom commands for memory:
- `/remember` - Explicitly log something to memory
- `/recall` - Search memory for specific information
- `/memory-sync` - Update and sync memory to GitHub

See [docs/memory-system.md](docs/memory-system.md) for detailed documentation.

### Using This Repo

1. Clone this repository to your development machine
2. Symlink or copy configurations to your project directories as needed
3. Customize configurations based on your workflow
4. At the start of each session, Claude reads memory logs to recall context

## Contributing

Feel free to add new configurations, prompts, or documentation that could be useful across projects.

## Server Setup

This configuration is maintained on a server with:
- Public-facing IP address
- GitHub CLI (gh) installed and authenticated
- Access to create repositories under the drakyn-ai organization
