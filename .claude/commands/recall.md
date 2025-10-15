# Recall Command

This command searches the memory system for specific information.

## What to do:

1. Search through memory files for the requested information:
   - memory/logs/session-log.md - Session history
   - memory/context/current-projects.md - Project info
   - memory/context/*.md - Other context files
2. Present relevant information to the user
3. If not found, let the user know and offer to remember it for next time

## Usage:

The user will type `/recall [topic]` and you should search memory for that topic.

## Examples:

- `/recall python preferences` - Look for Python-related preferences
- `/recall project status` - Check current project statuses
- `/recall last deployment` - Find information about recent deployments
- `/recall API keys` - Search for API configuration notes (not the keys themselves)

## Response format:

If found: Present the relevant information clearly
If not found: "I don't have any memory about [topic]. Would you like me to remember something about it?"
