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

- An X API Bearer Token ([get one here](https://developer.x.com/en/portal/dashboard)) — Basic tier ($100/mo) or higher required

### Installation

Give Claude this link and ask it to install:

```
Install this skill for me: https://raw.githubusercontent.com/TurboGuo/x-writer-skill/main/x-writer-SKILL.md
```

Or [download `x-writer-SKILL.md`](https://raw.githubusercontent.com/TurboGuo/x-writer-skill/main/x-writer-SKILL.md) and add it to your skills manually.

| Platform | Where to put it |
|----------|----------------|
| **Claude Code** | `~/.claude/skills/x-writer-SKILL.md` |
| **Claude Desktop** | Customize > Skills > Add Skill, paste the file contents |
| **Claude.ai (Web)** | Projects > New Project > Instructions, paste the file contents |

### Configure

Open the skill and replace the two config values at the top:

```
BEARER_TOKEN: YOUR_BEARER_TOKEN_HERE
X_HANDLE: YOUR_X_HANDLE_HERE
```

Then just ask Claude to write posts for you — triggers on phrases like "draft tweets", "write posts in my style", "x writer", etc.

## Usage examples

- "Draft some tweets for me"
- "Write posts in my style about AI agents"
- "Generate X content"
- "Ghostwrite tweets"
- "Help me post on X"

## Security Considerations

> **Read this before using the skill.** There are a few risks to be aware of.

| Risk | Description | Mitigation |
|------|-------------|------------|
| **Plaintext API token** | Your X API Bearer Token is stored directly in the skill `.md` file. If you commit/push this file with your real token, it will be exposed publicly. | **Never commit the skill file with your real token.** Add `x-writer-SKILL.md` to `.gitignore` after configuring it. Rotate your token immediately if leaked. |
| **Token in shell history** | The skill runs `curl` commands with your Bearer Token as a flag. These may be logged in `~/.zsh_history` or `~/.bash_history`. | Periodically clear sensitive entries from your shell history, or prefix commands with a space (if `HIST_IGNORE_SPACE` is enabled) to prevent logging. |
| **Temp files are world-readable** | Fetched posts are saved to `/tmp/xwriter_posts.json`. On shared or multi-user systems, other users can read `/tmp/`. | Acceptable on personal machines. On shared systems, consider changing the output path to a user-owned directory with restricted permissions. |
| **Style profile persistence** | The optional Step 7 saves your style profile to a predictable path, which could be read by other local users. | Only save if needed. Use a path inside your home directory with `chmod 600`. |
| **X API rate limits / cost** | The skill calls the X API on every run. Excessive use can hit rate limits (429) or rack up costs on paid tiers. | The skill fetches at most 100 tweets per run. Be mindful of how often you trigger it. |

## How it works under the hood

The skill uses the X API to pull your recent posts, then performs a detailed style analysis covering tone, structure, vocabulary, topic clusters, and engagement patterns. When generating drafts, it matches your exact voice — post length, emoji usage, hashtag habits, language mixing, and more. Each draft includes verified source URLs for any data claims.

## License

MIT
