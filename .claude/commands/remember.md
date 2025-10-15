# Remember Command

This command explicitly logs information to the memory system.

## What to do:

1. Ask the user what they want you to remember
2. Determine the appropriate memory file to update:
   - General facts/decisions: memory/logs/session-log.md
   - Project-specific: memory/context/current-projects.md
   - Preferences: Create memory/context/preferences.md if needed
3. Update the relevant memory file(s) with the information
4. Commit the changes with a descriptive message
5. Confirm to the user what was remembered

## Format:

Add entries with timestamps and clear descriptions. Keep entries concise but informative.

## Example:

User says: "Remember that I prefer to use Python 3.11+ for new projects"

You should:
1. Add to memory/context/preferences.md (create if needed)
2. Format: "**Python Version**: Prefer Python 3.11+ for all new projects"
3. Commit with message: "docs: remember Python 3.11+ preference"
4. Confirm: "I'll remember that you prefer Python 3.11+ for new projects."
