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
├── prompts/              # Reusable prompts and templates
└── docs/                 # Documentation and guides
```

## Getting Started

### Claude Code Configuration

The `.claude` directory contains Claude Code specific configurations:

- **Custom Commands**: Add custom slash commands in `.claude/commands/`
- **Settings**: Configure Claude Code behavior in `.claude/settings.json`

### Using This Repo

1. Clone this repository to your development machine
2. Symlink or copy configurations to your project directories as needed
3. Customize configurations based on your workflow

## Contributing

Feel free to add new configurations, prompts, or documentation that could be useful across projects.

## Server Setup

This configuration is maintained on a server with:
- Public-facing IP address
- GitHub CLI (gh) installed and authenticated
- Access to create repositories under the drakyn-ai organization
