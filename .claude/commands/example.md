# Example Custom Command

This is an example of how to create a custom slash command for Claude Code.

## Usage

To use this command, type `/example` in your conversation with Claude Code.

## What it does

This command demonstrates the basic structure of a custom command. You can create your own commands by adding markdown files to the `.claude/commands/` directory.

## Creating Your Own Commands

1. Create a new `.md` file in `.claude/commands/`
2. The filename becomes the command name (e.g., `deploy.md` becomes `/deploy`)
3. Write the instructions or prompts you want Claude to follow
4. Use the command by typing `/commandname` in your conversation

## Example Commands You Might Want

- `/deploy` - Deploy the current project
- `/review` - Perform a code review
- `/test` - Run tests and fix any failures
- `/docs` - Generate or update documentation
