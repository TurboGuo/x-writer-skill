# X Writer — Claude Code Skill

A Claude Code skill that analyzes your X/Twitter writing style from your recent posts and generates draft tweets that sound like you.

## What it does

1. **Fetches your recent posts** (up to 100) via the X API
2. **Builds a style profile** — tone, structure, vocabulary, topics, engagement patterns
3. **Suggests topics** based on what you've been posting about and what gets engagement
4. **Researches fresh content** — searches X for high-traction posts and the web for latest data on your chosen topic
5. **Generates 3 draft posts** in your authentic voice, each with a different angle, complete with verified sources
6. **Iterates with you** — edit, regenerate, adjust tone, switch topics

No auto-posting. Human approval always required.

## Setup

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- An X API Bearer Token ([get one here](https://developer.x.com/en/portal/dashboard)) — Basic tier ($100/mo) or higher required

### Installation

1. Copy `x-writer-SKILL.md` into your Claude Code skills directory:
   ```bash
   cp x-writer-SKILL.md ~/.claude/skills/
   ```
2. Open the file and replace the two config values at the top:
   ```
   BEARER_TOKEN: YOUR_BEARER_TOKEN_HERE
   X_HANDLE: YOUR_X_HANDLE_HERE
   ```
3. In Claude Code, just ask it to write posts for you — the skill triggers automatically on phrases like "draft tweets", "write posts in my style", "x writer", etc.

## Usage examples

- "Draft some tweets for me"
- "Write posts in my style about AI agents"
- "Generate X content"
- "Ghostwrite tweets"
- "Help me post on X"

## How it works under the hood

The skill uses the X API to pull your recent posts, then performs a detailed style analysis covering tone, structure, vocabulary, topic clusters, and engagement patterns. When generating drafts, it matches your exact voice — post length, emoji usage, hashtag habits, language mixing, and more. Each draft includes verified source URLs for any data claims.

## License

MIT
